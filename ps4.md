# Problem Session 4 Personal Solution


## Question 2:

Fick Nury directs an elite group of n superheroes called the Revengers. He has heard that supervillian Sanos is making trouble on a distant planet and needs to decide whether to confront her.  Fick surveys the Revengers and compiles a list of n polls, where each poll is a tuple matching a different Revenger’s name with their integer opinion on the topic. Opinion +s means they are for confronting Sanos with strength s, while opinion −s means they are against confronting Sanos with strength s. Fick wants to generate a list containing the names of the log n Revengers having the strongest opinions (breaking ties arbitrarily), so he can meet with them to discuss. For this problem, assume that the record containing the polls is read-only access controlled (the material in classified), so any computation must be written to alternative memory. 

(1) Describe an $O(n)$-time algorithm to generate Fick’s list. 

Binary heaps DS has two ops: 1. build 2.delete_max. So we use $O(n)$ to build a list of all abs value of elements and then use $O(logn*logn)$ to conduct $logn$ times delete_max on this list in order to get a list of top $logn$ maximum nums.

(2) Now suppose Fick’s computer is only allowed to write to at most $O(log n)$ space.Describe an $O(n loglog n)$-time algorithm to generate Fick’s list. 

First, get top $logn$ elements to generate a set where each one's key is its opinion's abs value using time $O(logn)$, and then use $O(log(logn))$ to find minimum key and compare it to next one's key in remaining list, remove the smaller one and insert the bigger one until loop over all the list. Time cost is $O(nlog(logn)+logn)$.


## Question 3:
Stormen, Ceiserson, Livest, and Rein are four academics who wrote a very popular textbook in computer science, affectionately known as SCLR. They just found k first editions in their offices, and want to auction them off online for charity. Each bidder in the auction has a unique integer bidder ID and can bid some positive integer amount for a single copy (but may increase or decrease their bid while the auction is live). Describe a database supporting the following operations, assuming n is the number of bidders in the database at the time of the operation. For each operation, state whether your running time is worst-case, expected, and/or amortized.

```new_bid(d, b)``` | record a new bidder ID $d$ with bid $b$ in $O(log n)$ time
```update_bid(d, b)``` | update the bid of existing bidder ID $d$ to bid $b$ in $O(log n)$ time
```get_revenue()``` | return revenue from selling to the current $k$ highest bidders in $O(1)$ time 

Solution: For first two ops, we just use a set AVL tree or a hash table. For ```get_revenue()```, we apply following data structure. Build a set AVL tree with elements keyed by thier ID ```d```, and build a max-priority queue and a min-priority queue. Use $O(logn)$ time to ```remove``` smallest one of min-priority queue and select largest one of max-priority queue, compare them and insert the one larger into min-priority queue until largest k elements are in min-priority queue and we maintain its sum ```B```. With this data structure we have ```get_revenue()``` costs $O(1)$. After implementing this data structure, we implement ```new_bid(d, b)``` through comparing ```b``` with smallest bid ```b'``` with bid ID ```d'```. Insert the larger one to and remove the smaller one from min-priority queue. Recompute ```B```. This costs $O(logn)$. 

To implement ```update_bid(d, b)```, we firstly remove ```b``` with id ```d```, then add max of max-priority queue, recompute ```B``` and conduct ```new_bid(d, b)``` to add it. This costs $O(logn)$. 

To implement ```get_revenue()```, we just compute ```B```, which takes $O(1)$.