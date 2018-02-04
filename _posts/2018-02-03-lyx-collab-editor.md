---
layout: post
title:  "Lyx: let's make it distributed"
date:   2018-01-25 12:21:59 -0500
categories: lyx distributed systems gsoc
---
## Introduction
This was my first project on Distributed Systems. It doesn't have all the delicious flavours of redundancy, scheduling, scalability etc. but it does deal with consensus, and I didn't even realise it at the time. This was my Google Summer of Code 2014 project. Briefly, GSoC is an initiative to encourage Open Source development in Students. Also, dedicated mentors are assigned to help students succeed. I finished this project successfully in the span of 4 months with the help of my extremely supportive mentor. This was one of the most significant turning points of my life, because I understood the true potential and scope of a career in Computer Science and how fun and interesting it can be.

{% include toc.html %}


### What is LyX?
![Lyx Logo]({{ "/assets/lyx-collab-editor/lyx_logo.png" | absolute_url }})

LyX is an open source Latex editor, where users can construct beautiful documents with just the powerful GUI, without having to know the intricacies of Latex.

### What are we trying to do?
Turn it into collaborative editor. Just like Google Doc, CollabEdit etc. This way multiple users can work on the same document over the internet.

## Some Background

### LyX Lingo
![LyX Architecture]({{ "/assets/lyx-collab-editor/lyx_architecture.png" | absolute_url }})

- This image shows how Lyx architecture is.
- Buffer
  - Holds pure raw text document. No functionality for editing (no cursor, no selection, no undo/redo)
- BufferView
  - Works on top of Buffer
  - Provides functionality for editing such as cursor, selection etc.
- LFUN
  - Any functionality in Lyx.
  - Represented as a string such as LFUN_COLLABORATE_CONNECT
  - Actual actions are taken care in "dispatcher"
- Cursor
  - Indicates location where BufferView is being edited currently
  - Represented by
    - Cell Index (row, column)
    - Paragraph Offset(which paragraph)
    - Position (position inside a paragraph)

### Remote BufferView
- Now if 2 users want to work on a document, how do we do that?
  - Keep 2 cursors inside a BufferView?
    - Would mean changing a lot of stable BufferView code.
    - Would have to handle the behaviour of all other LFUNs for the second cursor.
    - Error-prone.
  - Keep 2 BufferViews?
    - Much Simpler, no need to change BufferView Code.
    - Default behaviour for second cursor is already handled.

#### What is remote BufferView?
![Remote BufferView Concept]({{ "/assets/lyx-collab-editor/remote_bufferview.png" | absolute_url }})

For this project I had used simple TCP connection in order to connect two computers. Let's say there are 2 users. Each user will have local buffer and local BufferView, this is default behaviour. We introduce another BufferView for the second/remote user called "Remote BufferView". Any LFUNs that are dispatched onto this remote users local BufferView will be sent through TCP onto local users computer and dispatched on local user's remote BufferView. We use this main principle to create Collaborative Editor.

#### Putting it together
![Complete collaborative Concept]({{ "/assets/lyx-collab-editor/collab_concept.png" | absolute_url }})

- Each client is identified by an numeric id: ID
- Every client holds remote BufferView for every other client.
- Changes made by a client (LFUN) are forwarded to every other client through the server (ID, LFUN).
- Upon receiving, the client will dispatch it on remote bufferview for ID
- When a new client connects to the cluster, gets an identifier and the document.
- This ideas are easy to port over chat based protocol like xmpp.

### Need For Version Control
When a LFUN is dispatched on a remote BufferView, it acts on a version of the document that might be slightly different, as modified by the local user concurrently. It is important to clarify which revision of the document each LFUN applies to. Following 2 simple examples (where VCS is missing) show why VCS is vital.

A failure scenario can be say User 1 and User 2's cursors are at the end of a para. Now U1 starts typing some characters and U2 moves it's cursor 'right' before receiving those LFUNs. U2's cursor will be in next paragraph, where as his remote BufferView's cursor will stay in the previous paragraph.

Another example, User1 is editing in paragraph 4, User2 deletes paragraph 2. User1's cursor will still be in paragraph 4, which is incorrect.

Working of VCS/ History Table is shown here.
![Version Control System or History Table]({{ "/assets/lyx-collab-editor/vcs.png" | absolute_url }})

## Approaches

### Approach 1: send(LFUN, target_version, current_version)
This was my initial approach.
![First Approach]({{ "/assets/lyx-collab-editor/first_approach.png" | absolute_url }})

Each machine will have
- 1 Buffer
- 1 Local BufferView
- Multiple Remote BufferViews (as established before)
- Each Remote BufferView will have past versions of its cursor, numbered based on Local Bufferview's version.
- Local Bufferview changes will adjust remote bufferview's cursor, and enqueue a new Version.
- Remote machine will send (LFUN, target_version, current_version)
  - LFUN -> is an action
  - target_version -> Latest Local version of local bufferview that remote Bufferview knows about.
  - current_version -> For Local to synchronise with remote. Next time local is sending a LFUN to remote, it will send target as this number.

Problems:
- This had a very complicated implementation.
- The responsibility of updating remote bufferview's version by local was unnecessary.
- What to do if there are multiple remote bufferviews? Who will update remote bufferview 1's version, if remote bufferview 2 made some changes.

This Solution Didn't Work out. I was trying this for one month. But at the end there was always a new corner case that popped up. My mentors was travelling so he was offline during this time. GSoC was going to be a failure. When he came online, I explained the situation to him. The next day he gave me another solution. ONE HOUR, that's all that he required. I was inspired by his intelligence and the ingenuity of this solution. I am motivated till date to become that good.

### Approach 2: send(LFUN, target_version, current_version, cursor)
Each machine will have
- 1 Buffer
- 1 Local BufferView
- Remote BufferViews
- This Time, remote BufferViews do not hold history.
- Just the Local BufferView holds history of the changes it did.
- When a remote LFUN is received, it's cursor is adjusted based on local changes (after target_version) and dispatched.

To elaborate a little more for single machine:
- local user of machine 1
  - Inserts a character 'S' at 5th position in first para.
    - STEP 1: a new entry is made in the History Table of local bufferview (CHAR_IN_S, (5,0), 1)
      - CHAR_IN_S is LFUN for inserting S
      - (5,0) is cursor location(index, para), meaning S was inserted at 5th index in 0th paragraph
      - 1 is the Delta of the change, ie. just 1 character was inserted.
    - STEP 2: send the LFUN to the remote BufferView
      - (CHAr_IN_S, (5,0), machine_1)
  - A timer checks if there are any incoming LFUNs from remote
     - lets say there is one (CHAR_IN_Z, (8,0), machine_2)
     - (8,0) will get adjusted because a char 'S' was inserted at (5,0)
     - (8,0) will get adjusted to (9,0)
     - LFUN will be dispatched on the remote bufferview.
The image tries to explain above steps.

![Second Approach]({{ "/assets/lyx-collab-editor/second_approach.png" | absolute_url }})


### Some other details
- Connection is raw TCP Socket Based
  - Receiver has a QTimer (QT based) which checks if there is incoming LFUN.
- Local BufferView has a list of Remote BufferViews
  - A new Remote BufferView is added when a client connects
  - Each Remote BufferView has a socket Connection to the remote machine.
- Local BufferView has one TCP connection to its remote BufferView.
- Each Sent LFUN also has:
  - Current Version: to synchronise so that next requests can be targeted to this Current Version.
  - Anchor: to support selection.
- The code also contains Serialisers and Deserialisers, for converting LFUNs and Cursors to be sent over the network.


## Results:
Why write, when I can show you. The delay is significantly long, still the document ends up in a consistent state, YAAAY.

This is what the result looks like.
<iframe width="420" height="315" src="https://www.youtube.com/embed/Mh-1OL7I5qE" frameborder="0" allowfullscreen></iframe>

I haven't described supporting **Selections** in this blog, but the results are here.
<iframe width="420" height="315" src="https://www.youtube.com/embed/Lrv5pOsB2vQ" frameborder="0" allowfullscreen></iframe>


## Links
- [My GSOC Proposal]({{ "/assets/lyx-collab-editor/GSoc14.pdf" | absolute_url }})
- [My Submission]({{ "/assets/lyx-collab-editor/gsoc_eval.patch" | absolute_url }})
