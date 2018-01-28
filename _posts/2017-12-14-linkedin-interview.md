---
layout: post
title:  "Linkedin: An infuriating interview experience"
date:   2017-12-14 12:21:59 -0500
categories: linkedin interview
---
{% include toc.html %}


## TL;DR
  - Fantastic position - totally interested
  - Awesome Interviews - I nailed them
  - Large gap in between, Holiday Season
  - Recruiter did not inform me about the status
  - Position filled up! ... not even considered for team-matching.
  - No feedback.
  - (Oh! and I had an exam on the same day as my interview.. had to sacrifice some marks.)

**Company** | Linkedin
**Position** | Intern - Systems and Infrastructure Engineer
**Interviewer** | :star::star::star::star:/5
**Time** | 45 Minutes each
**Rounds** | 2
**Offer**  | No
**NDA** | No



## The Position
I am interested in the field of Distributed Systems. This was the one thing that made me break the deadlock of comfy-routine life at Directi. I took an excellent Distributed Systems course in my first term too. When I saw that Linkedin opened up the position,Systems And Infrastructure Engineer Intern, I did not hesitate asking for a favour from my friend for a referral. Linkedin, the creator of Kafka and Samza, would have given me so many opportunities to work on very interesting Distributed Systems.

## The Interviews
The recruiter called me up asking me about my interests and we talked about the position. I was given a window of one week to schedule my interview. I pushed the date as much as I can, but had to place it on the day of my exam because that was the latest I could interview.

There were two rounds of interviews both based on Algorithms and Data Structures. The interviewers were nice and helped me settle down.

### Round 1
- General Intro
- Interviewer asks me which area I like, DS or Algo.
  - I said DS
- **Question** Design a stack with `push()`, `pop()`, `peekMax()`, `popMax()`
  - My solutions:
    - BruteForce
      - O(1) Space Complexity, O(1) Time Complexity for push,pop, O(N) Time complexity for PeekMax, PopMax
      - Approach: A normal Stack. PeekMax and Popmax will require traversing the array.
    - 2 Stacks
      - O(N) Space Complexity, O(1) Time Complexity for Push, pop, Peekmax, O(N) for Popmax
      - Approach: 2 Stacks, the extra stack keeps track of maximum. Popmax might pop bottom element which will require refilling the max-stack, hence O(N).
    - A special heap
      - O(N) Space Complexity, O(log n) Time Complexity for Push, Pop, PopMax. O(1) for PeekMax.
      - Recall Prim's MST, the special heap data structure. See [here](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-mst-for-adjacency-list-representation/).
      - The Special Heap Data Structure is a combination of Heap and HashMap.
      - This is the Most Optimal Solution.
  - The interviewer seemed impressed.

### Round 2
 - No Intro.
 - Two interviewers, one shadowing the other.
 - **Question** Check if two Linked Lists merge.
 - two single-linked-lists heads are given, write a function that returns true if the two linked lists merge at some point.
 - This was a nice discussion based round and the interview propagated into detailed corner cases.
 - My Solution
  - BruteForce
    - O(N*M) TC, O(1) SC, for every node in LL1 check if any node in LL2 is the same.
  - HashSet
    - O(N) + O(M) TC, O(N) SC
    - Traverse one LL, mark nodes in a Hashset, traverse second and check if the node exists in the hashset.
    - **Follow-up** What if one linkedlist is infinitely long? and the merge happens at the beginning of the LL.
      - Changed Solution to ZigZag-based
      - Each LL is moved at each turn.
      - Same hash-map based approach, but this time both LL check on every move if the node has been seen before.
      -  **Follow-up** What if there is a loop?
        - Modified Solution to handle this case.
        - From a birds eye view:
          - Hashmap stores the LL owner of a node.
          - on each move:
            - Node has been seen before and Owner is the same stop moving this LL.
            - Node has been seen before and Owner is different, return True.
            - Node has not been seen before, store in hashSet with correct owner.
        - AAAh!!! I know I am not very expressive in describing the solution, but.. if you want to learn more, email me.
  - The interviewer seemed happy.
  - And I am 100% sure, my evaluation would be positive given the depth the discussion went into for 45 minutes and I was able to successfully code it too.


## The Misadventure
I knew I did well in the interviews. And I was eager for the position. So I contacted the recruiter after 3 days (17 Dec 2017), and I got to know the hiring committee has gone for Holidays, "expect no replies before new year". OK, sounds reasonable.

The holidays went so slowly, I was so excited.. so eager to hear the results and ready to cheer afterwards.

I contacted the recruiter back again on 3rd January, this time being explicit about the dates and I get an open ended response "There is no particular fixed date. I will let you know once the hiring committee makes the decision.". I trusted the recruiter to push my application forward.

I didn't want to seem needy and keep annoying the recruiter with pesky emails, so I laid low. One week went by .. *no response*. Another week.. again *no response*. Mind you, I was expecting a positive response, so everyday I would think about Linkedin.

Then one day, I noticed (on Linkedin) that the recruiter has changed team.. she is no longer a recruiter. Surely, she would've submitted my application to the hiring committee. I sent another email immediately on 23 January, this time being even more explicit about how the interviews went good and how the position excites me and how I am still waiting to hear back.

After two days I get a response. **From another HR**. "Unfortunately at this time, we are not able to move forward as we were not able to complete the team-matching process. I do want to thank you so much for your patience."

PATIENCE!!! Oh my! ... you are most definitely WELCOME!! I LOVE having to sacrifice my exams, prepare day and night for the interviews, get excited aimlessly, and yeah! wait enthusiastically for 1 and half months for NO REASON at all.

Just to add to the injury, I asked for some feedback about how I did in the interviews, No Response again!

Needless to say this was a very infuriating experience for me and I feel disrespected.

Would stay away from Linkedin in the future.

## Lesson I Learned
- Prepare for the interview with all the efforts.
- Do not expect anything in return.
- Forget and move on.
- If things are going to work out, they will.. no point thinking about it and wasting time.
- Things are not always in your control.
