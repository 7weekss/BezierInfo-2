# 求极值: 求根
现在我们（至少初步地）理解了分量函数，可以通过求解方程 B'(t) = 0，找到分量函数的最大和最小值，从而确定贝塞尔曲线的极值点。我们已经看到贝塞尔曲线的导数是一个更简易的贝塞尔曲线，但是这个等式该如何解呢？挺简单的，其实，直到我们导数的阶数高于三...那时候就会变得很难。但让我们先从简单的开始吧：


### 二次曲线: 线性导数.


二次贝塞尔曲线的导数是一条线性贝塞尔曲线，在两项之间插值。这就是说找到 “这条线在哪里等于0” 只需将其改写为 `t` 的函数，再求解。首先用[导数](#derivatives)章节所提及的规则把我们的二次贝塞尔变成一个线性贝塞尔函数：


\[
\begin{aligned}
  B'(t) = a(1-t) + b(t) &= 0,\\
  a - at + bt &= 0,\\
  (b-a)t + a &= 0\\
\end{aligned}
\]


然后通过基本的代数运算，将其转化为关于 `t` 的解：


\[
\begin{aligned}
  (b-a)t + a &= 0,\\
  (b-a)t &= -a,\\
  t &= \frac{-a}{b-a}\\
\end{aligned}
\]


完成.


[特例](https://en.wikipedia.org/wiki/Caveat_emptor#Caveat_lector)：如果 `b-a` 等于0，无解，也不应尝试除法。


### 三次曲线: 二次方程.
三次贝塞尔曲线的导数是一个二次贝塞尔曲线，所以为了求一个二次函数的根，可以用[二次方程](https://zh.wikipedia.org/wiki/%E4%BA%8C%E6%AC%A1%E6%96%B9%E7%A8%8B)。若你已经知道，你或许会想起。若没有学过，二次方程像这样：


\[
  \textit{已知}~f(t) = at^2 + bt + c,~f(t)=0 ~\textit{当}~ t = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\]


所以，如果可以把贝塞尔分量函数改写为普通的多项式方程，这就基本上完成了：只需把实数值代入二次方程，检查根号值是否为负值（若是，没有根）再计算出两个数值（因为有加减符号，有两个答案）。任何在0和1之间的数值是一个对贝塞尔曲线重要的根，其它的不相关（因为贝塞尔曲线只在区间[0,1]上定义）。那么，该如何转换呢？


首先，用[导数](#derivatives)章节所提及的规则把我们的三次贝塞尔变成一个二次贝塞尔：


\[
\begin{array}{l}
  B(t)~\textit{使用 uses}~\{ p_1,p_2,p_3,p_4 \} \\
  B'(t)~\textit{使用 uses}~\{ v_1,v_2,v_3 \},~\textit{其中 where}~v_1 = 3(p_2-p_1),~v_2 = 3(p_3-p_2),~v_3 = 3(p_4-p_3)
\end{array}
\]


然后，用*v*的数值，我们可以找到*a*，*b*，和*c*的数值：


\[
\begin{aligned}
  B'(t) &= v_1(1-t)^2 + 2v_2(1-t)t + v_3t^2 \\
  ... &= v_1(t^2 - 2t + 1) + 2v_2(t-t^2) + v_3t^2 \\
  ... &= v_1t^2 - 2v_1t + v_1 + 2v_2t - 2v_2t^2 + v_3t^2 \\
  ... &= v_1t^2 - 2v_2t^2 + v_3t^2 - 2v_1t + v_1 + 2v_2t \\
  ... &= (v_1-2v_2+v_3)t^2 + 2(v_2-v_1)t + v_1
\end{aligned}
\]


这就会给我们三个用 `v` 来定义的系数 {a, b, c}。`v`的值是我们原坐标值的表达式，所以我们可以通过代换得到：
This gives us three coefficients {a, b, c} that are expressed in terms of `v` values, where the `v` values are expressions of our original coordinate values, so we can do some substitution to get:


\[
\begin{aligned}
  a &= v_1-2v_2+v_3 = 3(-p_1 + 3p_2 - 3p_3 + p_4) \\
  b &= 2(v_2-v_1) = 6(p_1 - 2p_2 + p_3) \\
  c &= v_1 = 3(p_2-p_1)
\end{aligned}
\]


小事一桩。这样就可以把这些数值插入二次方程，非常简单的找到根。
Easy-peasy. We can now almost trivially find the roots by plugging those values into the quadratic formula.


因为是一个三次曲线，二次导数是有意义的。可以通过计算出一次导数的导数来找到它。
And as a cubic curve, there is also a meaningful second derivative, which we can compute by simply taking the derivative of the derivative.


### 四次曲线: 卡尔达诺公式


我们目前还没深入了解，但下一步会是一个四次贝塞尔曲线。和预期的一样，导数是一个三次函数，事情会变的更复杂。三次函数，和四次函数一样，没有一个”简单”的公式来求根，而是需要经过多次变形，改写成某种形式之后，才能开始尝试求解。
We haven't really looked at them before now, but the next step up would be a Quartic curve, a fourth degree Bézier curve. As expected, these have a derivative that is a cubic function, and now things get much harder. Cubic functions don't have a "simple" rule to find their roots, like the quadratic formula, and instead require quite a bit of rewriting to a form that we can even start to try to solve.


在16世纪，
Back in the 16<sup>th</sup> century, before Bézier curves were a thing, and even before _calculus itself_ was a thing, [Gerolamo Cardano](https://en.wikipedia.org/wiki/Gerolamo_Cardano) figured out that even if the general cubic function is really hard to solve, it can be rewritten to a form for which finding the roots is "easier" (even if not "easy"):


\[
  \begin{aligned}
    \textit{非常难：解 very hard: solve } & at^3 + bt^2 + ct + d = 0 \\
    \textit{更简单：解 easier: solve } & t^3 + pt + q = 0
  \end{aligned}
\]


We can see that the easier formula only has two constants, rather than four, and only two expressions involving `t`, rather than three: this makes things considerably easier to solve because it lets us use [regular calculus](https://www.wolframalpha.com/input/?i=t^3+%2B+pt+%2B+q) to find the values that satisfy the equation.


Now, there is one small hitch: as a cubic function, the solutions may be [complex numbers](https://en.wikipedia.org/wiki/Complex_number) rather than plain numbers... And Cardano realised this, centuries before complex numbers were a well-understood and established part of number theory. His interpretation of them was "these numbers are impossible but that's okay because they disappear again in later steps", allowing him to not think about them too much, but we have it even easier: as we're trying to find the roots for display purposes, we don't even _care_ about complex numbers: we're going to simplify Cardano's approach just that tiny bit further by throwing away any solution that's not a plain number.


So, how do we rewrite the hard formula into the easier formula? This is explained in detail over at [Ken J. Ward's page](https://trans4mind.com/personal_development/mathematics/polynomials/cubicAlgebra.htm) for solving the cubic equation, so instead of showing the maths, I'm simply going to show the programming code for solving the cubic equation, with the complex roots getting totally ignored, but if you're interested you should definitely head over to Ken's page and give the procedure a read-through.


<div class="howtocode">


### Implementing Cardano's algorithm for finding all real roots


The "real roots" part is fairly important, because while you cannot take a square, cube, etc. root of a negative number in the "real" number space (denoted with ℝ), this is perfectly fine in the ["complex" number](https://en.wikipedia.org/wiki/Complex_number) space (denoted with ℂ). And, as it so happens, Cardano is also attributed as the first mathematician in history to have made use of complex numbers in his calculations. For this very algorithm!


```
// A helper function to filter for values in the [0,1] interval:
function accept(t) {
  return 0<=t && t <=1;
}


// A real-cuberoots-only function:
function cuberoot(v) {
  if(v<0) return -pow(-v,1/3);
  return pow(v,1/3);
}


// Now then: given cubic coordinates {pa, pb, pc, pd} find all roots.
function getCubicRoots(pa, pb, pc, pd) {
  var   a = (3*pa - 6*pb + 3*pc),
        b = (-3*pa + 3*pb),
        c = pa,
        d = (-pa + 3*pb - 3*pc + pd);


  // do a check to see whether we even need cubic solving:
  if (approximately(d,0)) {
    // 这不是一个三次曲线。 this is not a cubic curve.
    if (approximately(a,0)) {
      // 也不是一个四次曲线。 in fact, this is not a quadratic curve either.
      if (approximately(b,0)) {
        // 其实，根本没有根。in fact in fact, there are no solutions.
        return [];
      }
      // 线性解 linear solution
      return [-c / b].filter(accept);
    }
    // 二次解 quadratic solution
    var q = sqrt(b*b - 4*a*c), 2a = 2*a;
    return [(q-b)/2a, (-b-q)/2a].filter(accept)
  }


  // at this point, we know we need a cubic solution.


  a /= d;
  b /= d;
  c /= d;


  var p = (3*b - a*a)/3,
      p3 = p/3,
      q = (2*a*a*a - 9*a*b + 27*c)/27,
      q2 = q/2,
      discriminant = q2*q2 + p3*p3*p3;


  // and some variables we're going to use later on:
  var u1, v1, root1, root2, root3;


  // three possible real roots:
  if (discriminant < 0) {
    var mp3  = -p/3,
    mp33 = mp3*mp3*mp3,
    r    = sqrt( mp33 ),
    t    = -q / (2*r),
    cosphi = t<-1 ? -1 : t>1 ? 1 : t,
    phi  = acos(cosphi),
    crtr = cuberoot(r),
    t1   = 2*crtr;
    root1 = t1 * cos(phi/3) - a/3;
    root2 = t1 * cos((phi+2*pi)/3) - a/3;
    root3 = t1 * cos((phi+4*pi)/3) - a/3;
    return [root1, root2, root3].filter(accept);
  }


  // three real roots, but two of them are equal:
  if(discriminant === 0) {
    u1 = q2 < 0 ? cuberoot(-q2) : -cuberoot(q2);
    root1 = 2*u1 - a/3;
    root2 = -u1 - a/3;
    return [root1, root2].filter(accept);
  }


  // one real root, two complex roots
  var sd = sqrt(discriminant);
  u1 = cuberoot(sd - q2);
  v1 = cuberoot(sd + q2);
  root1 = u1 - v1 - a/3;
  return [root1].filter(accept);
}
```


</div>


And that's it. The maths is complicated, but the code is pretty much just "follow the maths, while caching as many values as we can to prevent recomputing things as much as possible" and now we have a way to find all roots for a cubic function and can just move on with using that to find extremities of our curves.


And of course, as a quartic curve  also has meaningful second and third derivatives, we can quite easily compute those by using the derivative of the derivative (of the derivative), just as for cubic curves.




### Quintic and higher order curves: finding numerical solutions


And this is where thing stop, because we _cannot_ find the roots for polynomials of degree 5 or higher using algebra (a fact known as [the Abel–Ruffini theorem](https://en.wikipedia.org/wiki/Abel%E2%80%93Ruffini_theorem)). Instead, for occasions like these, where algebra simply cannot yield an answer, we turn to [numerical analysis](https://en.wikipedia.org/wiki/Numerical_analysis).


That's a fancy term for saying "rather than trying to find exact answers by manipulating symbols, find approximate answers by describing the underlying process as a combination of steps, each of which _can_ be assigned a number via symbolic manipulation". For example, trying to mathematically compute how much water fits in a completely crazy three dimensional shape is very hard, even if it got you the perfect, precise answer. A much easier approach, which would be less perfect but still entirely useful, would be to just grab a buck and start filling the shape until it was full: just count the number of buckets of water you used. And if we want a more precise answer, we can use smaller buckets.


So that's what we're going to do here, too: we're going to treat the problem as a sequence of steps, and the smaller we can make each step, the closer we'll get to that "perfect, precise" answer. And as it turns out, there is a really nice numerical root-finding algorithm, called the [Newton-Raphson](https://en.wikipedia.org/wiki/Newton-Raphson) root finding method (yes, after *[that](https://en.wikipedia.org/wiki/Isaac_Newton)* Newton), which we can make use of. The Newton-Raphson approach consists of taking our impossible-to-solve function `f(x)`, picking some initial value `x` (literally any value will do), and calculating `f(x)`. We can think of that value as the "height" of the function at `x`. If that height is zero, we're done, we have found a root. If it isn't, we calculate the tangent line at `f(x)` and calculate at which `x` value _its_ height is zero (which we've already seen is very easy). That will give us a new `x` and we repeat the process until we find a root.


Mathematically, this means that for some `x`, at step `n=1`, we perform the following calculation until `f<sub>y</sub>(x)` is zero, so that the next `t` is the same as the one we already have:


\[
  x_{n+1} = x_n - \frac{f_y(x_n)}{f'_y(x_n)}
\]


(The Wikipedia article has a decent animation for this process, so I will not add a graphic for that here)


Now, this works well only if we can pick good starting points, and our curve is [continuously differentiable](https://en.wikipedia.org/wiki/Continuous_function) and doesn't have [oscillations](https://en.wikipedia.org/wiki/Oscillation_(mathematics)). Glossing over the exact meaning of those terms, the curves we're dealing with conform to those constraints, so as long as we pick good starting points, this will work. So the question is: which starting points do we pick?


As it turns out, Newton-Raphson is so blindingly fast that we could get away with just not picking: we simply run the algorithm from *t=0* to *t=1* at small steps (say, 1/200<sup>th</sup>) and the result will be all the roots we want. Of course, this may pose problems for high order Bézier curves: 200 steps for a 200<sup>th</sup> order Bézier curve is going to go wrong, but that's okay: there is no reason (at least, none that I know of) to _ever_ use Bézier curves of crazy high orders. You might use a fifth order curve to get the "nicest still remotely workable" approximation of a full circle with a single Bézier curve, but that's pretty much as high as you'll ever need to go.


### 总结:


So now that we know how to do root finding, we can determine the first and second derivative roots for our Bézier curves, and show those roots overlaid on the previous graphics. For the quadratic curve, that means just the first derivative, in red:


<graphics-element title="二次贝塞尔曲线的极值Quadratic Bézier curve extremities" width="825" src="./extremities.js" data-type="quadratic"></graphics-element>




And for cubic curves, that means first and second derivatives, in red and purple respectively:


<graphics-element title="三次贝塞尔曲线的极值Cubic Bézier curve extremities" width="825" src="./extremities.js" data-type="cubic"></graphics-element>



