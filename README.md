# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

# Solution

First, we should look at the amount of times mystery calls itself, which is 3. Then, we look at the for loops lengths which are: $n^2$, $n$, and $n^2$ in order. That means the total loop length is $n^5$. So, our reccurence relation should be:

$$T(n)=3T(\frac{n}{3})+n^5$$

Expand by substituting n/3:

   $T(n) = 3[3T(\frac{n}{9}) + (\frac{n}{3})^5] + n^5$
   
   $= 9T(\frac{n}{9}) + 3(\frac{n^5}{243}) + n^5$

Expand again:

   $T(n) = 9[3T(\frac{n}{27}) + (\frac{n}{9})^5] + 3(\frac{n^5}{243}) + n^5$
   
   $= 27T(\frac{n}{27}) + 9(\frac{n^5}{59049}) + 3(\frac{n^5}{243}) + n^5$

We can see a pattern forming at each step:
   - The coefficient of T gets multiplied by 3
   - The denominator of n/x gets multiplied by 3
   - We add another term with $n^5$ divided by increasing powers of 3

Abstracting to k steps, we get:

   $T(n) = 3^kT(\frac{n}{3^k}) + n^5(1 + \frac{1}{3^4} + \frac{1}{3^8} + ... + \frac{1}{3^{4k}})$

The recursion stops when $\frac{n}{3^k} \leq 1$, or when:
   $\frac{n}{3^k} = 1$
   
   $3^k = n$
   
   $k = \log_3(n)$

The sum converges to a constant because it's a geometric series with ratio < 1.
   So the dominant term will be $n^5$

Therefore: 

$$T(n) = O(n^5)$$

# Disclaimer

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.
