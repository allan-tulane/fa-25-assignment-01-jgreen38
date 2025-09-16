

# CMPS 2200 Assignment 1

**Name:**Justin Green


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not? 
.  Yes, 2^(n+1) is in O(2^n). 2^(n+1) = 2^1 * 2^n. To satisfy the Big O definition, we need to find a constant c such that 2 * 2^n <= c * 2^n for all n >= n0. If we select c = 2 and n0 = 1, then 2 * 2^n <= 2 * 2^n. Since the condtion holds, 2^(n+1) is in O(2^n).
.  
.  
.  
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  No, 2^(2^n) is not in O(2^n). To satisfy the Big O definition, we need to find a constant c such that 2^(2^n) <= c * 2^n for all n >= n^0. We can easily identify our growth ratio by dividing 2^(2^n) by 2^n. Our resulting growth ratio is 2^(2^n - n). We want to determine if there is a bound as n gets increasingly larger and approaches infinity to determine if 2^(2^n) is in O(2^n). However, 2^(2^n) grows much faster than 2^n because it grows at a double exponential rate (the exponent has an exponent) rather than at a single exponential rate. Because of this, there is no constant c that can satisfy the Big O definition since the growth ratio grows with no bound. Therefore, 2^(2^n) is not in O(2^n).
.  
.  
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  No, n^1.01 is not in O(log^2 n).
.  Again, we want to compare the growth rates by looking at the growth ratio, which is n^1.01/log^2(n). From this, we want to assess if there is a bound to the growth as n approaches infinity. Since n^1.01 grows faster than log^2 n, we will find that there is no bound and the ratio goes to infinity. Consequently, there is no constant c that will satisfy the Big O definition, so n^1.01 is not in O(log^2 n). 
.  
.  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  
.  Yes, n^1.01 is in Omega(log^2 n).
.  We are playing with omega here, so we have different parameters to meet in order to determine our answer. With the definition of omega, we want to find if there exists a constant c > 0 and n0 such that f(n) >= c * g(n). This is different from big O, which looks for f(n) <= c * g(n). We are looking at the same growth ratio from the last part of the question. However, since we are looking in the opposite direction, the ratio increasing to infinity works to our benefit. As we approach infinity, eventually n^1.01 will surpass log^2 n, so there exists a constant c that will satisfy n^1.01 >= c * log^2 n.
.  
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  No, sqrt(n) is not in O((log n)^3).
.  Similar to 1c, sqrt(n), or n^(1/2), grows faster than (log n)^3. Resultingly, as n approaches infinity, so does the growth ratio because of the lack of a bounding value n. We can draw the same conclusion that because of this, there is no constant c that satisfies sqrt(n) <= c * (log n)^3.
.  
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
.  Yes, sqrt(n) is in Omega((log n)^3). Similar to 1d, since we are looking in the opposite direction of the last question, our growth ratio going to infinity is good. It means that we will eventually find n such that sqrt(n) outgrows ((log n)^3), and this means there is some constant c that will satisfy sqrt(n) >= (log n)^3.


2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  

.  This function is a simple recursive Fibonacci implementation.
.  In our base case, if x <= 1, return x. This returns foo(0) = 0 and foo(1) = 1, which follows the base case rules of fibonacci.
.  In our recursive call, for values of x >= 2, we return foo(x) = foo(x-1) + foo(x-2). For foo(4), we have foo(3) + foo(2). foo(3) = foo(2) + foo(1). foo(2) = foo(1) + foo(0). foo(2) = 1 + 0 (base cases) = 1. foo(3) = 1 + 1 = 2. foo(4) = 2 + 1 = 3, so foo(4) will correctly return 3 when called.
.  
.  
.  
.  
.  
  

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  

.  The work is W(n) = O(n) and the work is S(n) = O(n). We iterate over each element of the list once and do O(1) work for each element. Since this is sequential, the work is also O(n) for the same reason.
.  
.  
.  
.  
.  
.  
.  
.  


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  
.  The work is W(n) = 2W(n/2) + O(1). We split our list in half, creating two seperate pieces that are n/2 length. We recursively call both n/2 length lists, which requires work W(n) = W(n/2) for both, totaling W(n) = 2W(n/2) just for our recursive calls. As stated before, visiting each element in a list requires O(1) work so our total comes out to W(n) = 2W(n/2) + O(1). Ultimately, this solves to equal W(n) = O(n) because the amount of work is dependent solely on the length of the list. The span is S(n) = 2S(n/2) + O(1) because we are performing our recursive calls in sequence. The left takes S(n) = S(n/2) and the right takes the same length of time, then add O(1) for the span of combining.
.  
.  
.  
.  
.  
.  
.  
.  
.  
.  


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

.  The work is still W(n) = 2W(n/2) + O(1), but the span is S(n) = S(n/2) + O(1) because parallelism does not impact work, but does impact the span of an algorithm. We no longer perform our recursive calls one after another. We, instead, perform them at the same time, allowing us to decrease our span from 2S(n/2) for the recursive calling step down to S(n/2) to complete them together. This changes the span from O(n) to O(log n) because log2(2 branches) = 1 parallel step, rather than 2 branches being done in 2 sequential steps. 
.  
.  
.  
.  
.  
.  
.  

