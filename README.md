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

$$T(n)=3T(\frac{n}{3})+n^5 $$

Using the master theorem $T_n= a T(\frac{n}{b})+f(n)$, we can see that $a=3$, $b = 3$, and $f(n)=n^5$. Which means $c_{\text{crit}} = \log_b(a) = \log_3(3) = 1$. Now we compare $n^{c_{\text{crit}}}$ to our function $f(n)$:

$n^1 ? n^5 \rightarrow n^1 < n^5$

Because $f(n)$ grows faster than $n^{c_{\text{crit}}}$, we use Case 3 of the master theorem. Therefore, our asymptotic bound is:

$$O(n^5)$$

# Disclaimer

I used [this](https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)) for the master theorem table.

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.
