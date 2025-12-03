# Problem Session 4 Personal Solution


## Question 2:

Fick Nury directs an elite group of n superheroes called the Revengers. He has heard that supervillian Sanos is making trouble on a distant planet and needs to decide whether to confront her.  Fick surveys the Revengers and compiles a list of n polls, where each poll is a tuple matching a different Revenger’s name with their integer opinion on the topic. Opinion +s means they are for confronting Sanos with strength s, while opinion −s means they are against confronting Sanos with strength s. Fick wants to generate a list containing the names of the log n Revengers having the strongest opinions (breaking ties arbitrarily), so he can meet with them to discuss. For this problem, assume that the record containing the polls is read-only access controlled (the material in classified), so any computation must be written to alternative memory. 

(1) Describe an $O(n)$-time algorithm to generate Fick’s list. 

Binary heaps DS has two ops: 1. build 2.delete_max. So we use $O(n)$ to build a list of all abs value of elements and then use $O(logn*logn)$ to conduct $logn$ times delete_max on this list in order to get a list of top $logn$ maximum nums.

(2) Now suppose Fick’s computer is only allowed to write to at most $O(log n)$ space.Describe an $O(n loglog n)$-time algorithm to generate Fick’s list. 

First, get top $logn$ elements to generate a set where each one's key is its opinion's abs value using time $O(logn)$, and then use $O(log(logn))$ to find minimum key and compare it to next one's key in remaining list, remove the smaller one and insert the bigger one until loop over all the list. Time cost is $O(nlog(logn)+logn)$.


## Question 3:
