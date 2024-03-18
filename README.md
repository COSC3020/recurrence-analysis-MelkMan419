[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
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

T(n)=1 if n<=1
3T(n/3) + n^5 else

Solve by substitution 

$T(n) = 3T(\frac{n}{3}) + n^5$<br>
$T(n) = 3(3T(\frac{n/3}{3}) + (\frac{n}{3})^5) + n^5$<br>
$T(n) = 3^2T(\frac{n}{3^2}) + \frac{n^5}{3^4} + n^5$<br>
$T(n) = 3^3T(\frac{n}{3^3}) + \frac{n^5}{3^5} + \frac{n^5}{3^4} + n^5$<br>

Looking at the pattern, we can see the recurrence relation is

$3^iT(\frac{n}{3^i}) + \displaystyle\sum_{j=0}^i \frac{n^5}{3^{i+2}}  + n^5$.<br>
To terminate the recurrence, $T(n)$ must be <= 1. <br>
According to the pattern, $T(1) = T(\frac{n}{3^i})$<br>
$\frac{n}{3^i} = 1$<br>
$n = 3^i$<br>
$i = \log_{3} n$ <- value of i when n = 1. <br>
Plugging it in: <br>
$3^{\log_{3} n}  * T(1) + \displaystyle\sum_{j=0}^{\log_{3} n} \frac{n^5}{3^{(\log_{3} n) + 2}} + n^5$<br>
Which simplifies to $n + \displaystyle\sum_{j=0}^{\log_{3} n}\frac{n^5}{n+2} + n^5$<br>

so the time complexity is $\Theta(n^5)$
