---
layout: post
title:  "What went wrong with my Facebook interview!"
date:   2018-01-08 12:21:59 -0500
categories: facebook interview
---
# Plot Twist: I cleared this Round
Sorry, about the misleading title. I was so sure I wasn't going to clear this round, but I did. I wrote this blog on the very day of my interview, frustrated with my performance.. Enjoy the rant!

**Company** | Facebook
**Position** | Intern - Production Engineer
**Interviewer** | :star::star::star::star:/5
**Time** | 45 Minutes
**Rounds** | 1
**Offer**  | No
**NDA** | No

## Mistake 1: Mind the role
The position I interviewed for is not Software Engineer, it's Production Engineer. Production Engineering does not involve 100% coding, but it's a hybrid software/ system engineering and requires thorough knowledge of Linux. The recruiter was very clear about first round being about Algorithms and Data Structures. From what I gathered from Glassdoor and Careercup, the first round was going to be easy. But during the interview I didn't mind this information. I was thinking with a unnecessarily complicated mindset, which we normally go with in a Software Engineering Interview. You know, **I need to find the most optimal possibly tricky solution**. This was my mistake.

## The Interview
I didn't sign any NDA, so I'm free to discuss my interview experience here. One thing that was unique about this interview was time constraint. 45 Minutes total interview length, 10 minutes were already gone in introduction, 5 minutes were reserved for asking the interviewer some questions, two questions were asked ,each were allotted 15 minutes.

### Question 1 (15 Minutes)
Given 2 CSV files data1.csv and data2.csv, such as
```
Dinosaur      , Pedal         , Feet length
Dilophosaurus , Bipedal       , 3.0        
Troodon       , quadrupedal   , 4.2        
Sauropoda     , Bipedal       , 4.1        
Archaeopteryx , quadrupedal   , 2.5      

Dinosaur      , Stride Length , Max Age    
Archaeopteryx , 13.0          , 15         
Sauropoda     , 12.2          , 22         
Dilophosaurus , 14.1          , 37         
Troodon       , 12.5          , 71     
```
and Given following formula for computing speed,

{% highlight Python%}
Speed = ((Feet length * Stride Length)/ (Pedal) ) * g
{% endhighlight %}


I had to print out the names of Dinosaurs in increasing order of their speed.

I solved the question but did two minor mistakes.
#### Used map
After Reading a line and splitting it with commas, I converted each content of the list to string, which was not required (as they are already in string format)
{% highlight Python%}
inputLineList = map(str, inputfile.readline().split(','))
{% endhighlight %}

#### Forgot Loop :expressionless:
I forgot the loop to read the contents of the file till the end. :shit:

### Question 2 (15 minutes)
There is a matrix with `.` and `X`, where `X` represents battleship, always of length 3. Battleship can be vertical or horizontal, never diagonal.
Given a function `bomb_at(i,j)`, returns `True` if battleship is present at (i,j) in the matrix.
Print the head, middle, tail coordinates of the battleship.

I asked a question to clarify, and as it turns out there will always be one battleship.
```
.........
.....X...
.....X...
.....X...
.........

```

After seeing this question, guess what my well-trained **monotonous** mind thought the solution would be? **Depth First Search**. And I began writing the solution. I wrote a recursive solution.. in around 8 minutes. But the solution didn't work because (i,j) was recursively calling (i+1,j),(i-1,j),(i,j+1),(i,j-1). And (i+1,j) will again call (i,j) internally.. leading to an infinite loop. One easy way to solve this is to manipulate original matrix, and replace `X` with `.` after its done.. but I do not have access to the matrix. So in the remaining 7 Minutes I started thinking about other solutions. But Time ran out while I was coding my other solution.


## Mistake 2: Read the question carefully, take time, think, then speak
The question descriptions were very long, I just glanced at the description and attacked the problem. I overlooked so many important details and had to change my code so many times to accommodate those details... this led to a waste of precious time.

Ok, another thing, this is something which has happened to me twice now. You know *How it is important to keep speaking as you think*, **Don't**, take time and then speak.

Why? Because interviewer can ask you to code your first instinct, which may be wrong or may not be optimal. This has happened before with A9, and happened again today with Facebook.

So I always go like this.. "The first thing that's popping up in my mind is... blah blah blah". And for Question 2, I said "Depth First Search". The interviewer replied "Sounds good!, start coding". And then I began coding, **Without even thinking about any other solutions**, and ended up trapping myself in a corner.

## Mistake 3: Ignore preconceived solutions / Start Afresh
After practicing for so long on Leetcode and geeksforgeeks, I began to start thinking in a particular way for particular set of problems. If its a graph than solutions should be of DFS/ BFS. If its a tree start thinking of recursion. You want to reduce space for matrix? use adjacency list (A9).
This was also the reason why I came up with the Depth First Search solution for Question 2. But after the interview I thought about the solution.. and with the following pieces of information
- Exactly 1 battleship
- Always length 3

The solution is as follows
{% highlight Python%}
  for i in range(grid_length):
    for j in range(grid_length):
      if bomb_at(i,j):
        print((i,j))
{% endhighlight %}

**THIS SIMPLE.**
