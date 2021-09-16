# CMPS 2200  Recitation 01

**Name (Team Member 1):**________Batu El__________  
**Name (Team Member 2):**_________________________

In this recitation, we will investigate asymptotic complexity. Additionally, we will get familiar with the various technologies we'll use for collaborative coding.

To complete this recitation, follow the instructions in this document. Some of your answers will go in this file, and others will require you to edit `main.py`.


## Setup
- Login to Github.
- Click on the assignment link sent through canvas and accept the assignment.
- Click on your personal github repository for the assignment (e.g., https://github.com/tulane-cmps2200/recitation-01-your_username).
- [Clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) the repository to your local device
- Complete the lab task 
- [Add, commit, and push](https://docs.github.com/en/github/managing-files-in-a-repository/managing-files-using-the-command-line/adding-a-file-to-a-repository-using-the-command-line) your completed lab back up to GitHub. 
  - You will need to issue `git add` for all files that you have modified, e.g., `main.py`, `README.md`, and any others that you modify as well.
  - For example, on the command line, in the same directory as your cloned lab:
```
$ git add main.py
$ git commit -m "Implement Required Functions"
$ git push origin main
```

You'll work with a partner to complete this recitation. You will be able to code together in the same `repl.it` instance. You can choose whose repl.it instance you will share. This person will click the "Share" button in their repl.it instance and email the lab partner.

## Turning in your work
- Only one team member needs to push your completed lab to github. 
- In the README.md file, include the name of the team members.


## Comparing search algorithms

We'll compare the running times of `linear_search` and `binary_search` empirically.

- [ ] 1. In `main.py`, the implementation of `linear_search` is already complete. Your task is to implement `binary_search`. Implement a recursive solution using the helper function `_binary_search`. 

- [ ] 2. Test that your function is correct by calling from the command-line `pytest main.py::test_binary_search`

- [ ] 3. Write at least two additional test cases in `test_binary_search` and confirm they pass.

- [ ] 4. Describe the worst case input value of `key` for `linear_search`? for `binary_search`? 

**TODO: your answer goes here**
the worst case input value of `key` for `linear_search` a key that is not in the list. This is because the algorithm has to iterate through all the elements before returning -1 to indicate that the key is not in the list. The runtime is O(N).
the worst case input values of `key` for `binary_search` is also any key that is not in the list. The runtime, however, is O(log(base 2)(N)).

- [ ] 5. Describe the best case input value of `key` for `linear_search`? for `binary_search`? 

**TODO: your answer goes here**
For linear search, the best case input value is the first element in the list, i.e. the element at index 0.
For binary search, the best case input value is the element in the middle of the list, i.e. the element is at index len(mylist)//2. Note the integer division operator rounds to the smaller integer (since indices only take positive values). 

- [ ] 6. Complete the `time_search` function to compute the running time of a search function. Note that this is an example of a "higher order" function, since one of its parameters is another function.

- [ ] 7. Complete the `compare_search` function to compare the running times of linear search and binary search. Confirm the implementation by running `pytest main.py::test_compare_search`, which contains some simple checks.

- [ ] 8. Call `print_results(compare_search())` and paste the results here:

**TODO: add your timing results here**
|            n |   linear |   binary |
|--------------|----------|----------|
|       10.000 |    0.002 |    0.004 |
|      100.000 |    0.004 |    0.002 |
|     1000.000 |    0.056 |    0.003 |
|    10000.000 |    0.572 |    0.005 |
|   100000.000 |    5.760 |    0.027 |
|  1000000.000 |   54.364 |    0.016 |
| 10000000.000 |  515.804 |    1.372 |

- [ ] 9. The theoretical worst-case running time of linear search is $O(n)$ and binary search is $O(log_2(n))$. Do these theoretical running times match your empirical results? Why or why not?

**TODO: your answer goes here**
|            n |   linear |   binary |  log(base2)(n) |   linear/n  | log(base2)(n)/binary  |
|--------------|----------|----------|----------------|-------------|-----------------------|
|       10.000 |    0.002 |    0.004 |   3.332        |   0.0002    |   833                 |
|      100.000 |    0.005 |    0.004 |   6.644        |   0.00005   |   1661                |
|     1000.000 |    0.056 |    0.005 |   9.966        |   0.000056  |   1993.2              |
|    10000.000 |    0.580 |    0.007 |   13.288       |   0.000058  |   1898.2              |
|   100000.000 |    6.044 |    0.015 |   16.61        |   0.000060  |   1107.3              |
|  1000000.000 |   54.697 |    0.016 |   19.93        |   0.000054  |   1245.625            |
| 10000000.000 |  499.331 |    0.019 |   23.253       |   0.000049  |   1223.8              |

The empirical results follow trends similar to theorethical findings. For example, linear runtime is close to n*00005, which is directly proportional to n. The binary runtime is approximately (log(base2)(n)/n)*1200. It is important to note that these relationships are less clear for smaller n because the majority of the runtime is taken by lines with fixed runtime in the algoritm. 


- [ ] 10. Binary search assumes the input list is already sorted. Assume it takes $\Theta(n^2)$ time to sort a list of length $n$. Suppose you know ahead of time that you will search the same list $k$ times. 
  + What is worst-case complexity of searching a list of $n$ elements $k$ times using linear search? **TODO: your answer goes here** 
  k*O(n) = O(k*n)
  + For binary search? **TODO: your answer goes here**
  k*O(log_2(n)) = O(k*log_2(n))
  + For what values of $k$ is it more efficient to first sort and then use binary search versus just using linear search without sorting? **TODO: your answer goes here**
  whenever linear search time > sorting time + binary search time
  
  k*O(n) > Theta(n^2) + k*O(log_2(n))
  -> alpha*k*n > theta(n^2) + beta*k*log_2(n)
  -> alpha*k*n - beta*k*log_2(n) > theta(n^2)
  -> k* (alpha*n - beta*log_2(n)) > theta(n^2)
  -> k > theta(n^2) / (alpha*n - beta*log_2(n))
  
  We can take alpha=beta=1, we have 
  k > theta(n^2) / (n - log_2(n))
