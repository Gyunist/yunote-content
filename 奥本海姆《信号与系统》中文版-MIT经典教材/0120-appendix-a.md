**附 录 部分分式展开**

### A.1 引 言 {#sec:A-1}

本附录的目的是阐述部分分式展开方法。在信号与系统的研究中，这一方法是非常有用的；尤其是在求傅里叶反变换、拉普拉斯反变换或z反变换，以及分析由线性常系数微分方程或差分方程表征的LTI系统时，显得特别有用。部分分式展开法就是把一个由两个多项式之比构成的函数，展开成一些形式上相同的简单项的线性组合。在这个线性组合中，确定系数是获得部分分式展开要解决的基本问题。将会看到，这个问题在代数中能用一种“簿记”的形式很方便解决的一个相当直接的问题。

为了说明基本想法和部分分式展开的基本法则。现考虑在6.5.2节中讨论过的二阶连续时间LTI系统的分析问题。其微分方程为

$$
\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}+2\zeta\omega_{n}\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+\omega_{n}^{2}y\left(t\right)=\omega_{n}^{2}x\left(t\right)
$$

该系统的频率响应是

$$
H(\mathrm{j}\omega)=\frac{\omega_{n}^{2}}{(\mathrm{j}\omega)^{2}+2\zeta\omega_{n}(\mathrm{j}\omega)+\omega_{n}^{2}}
$$

或者，若将分母因式分解，有

$$
H(\mathrm{j}\omega)=\frac{\omega_{n}^{2}}{(\mathrm{j}\omega-c_{1})(\mathrm{j}\omega-c_{2})}
$$

其中

$$
c_{1}=-\zeta\omega_{n}+\omega_{n}\sqrt{\zeta^{2}-1}
$$

$$
c_{2}=-\zeta\omega_{n}-\omega_{n}\sqrt{\zeta^{2}-1}
$$

有了 $ H(j\omega) $ 之后，就可以回答许多有关该系统的问题。例如，为了求出该系统的单位冲激响应，回忆一下，对于任何实部 $ \mathcal{R}_{0}\{s\} < 0 $ 的 $ \alpha $

$$
x_{1}(t)=\mathrm{e}^{a t}u(t)
$$

的傅里叶变换为

$$
X_{1}(\mathrm{j}\omega)=\frac{1}{\mathrm{j}\omega-\alpha}
$$

而如果

$$
x_{2}(t)=t\mathrm{e}^{a t}u(t)
$$

那么

$$
X_{2}(\mathrm{j}\omega)=\frac{1}{(\mathrm{j}\omega-\alpha)^{2}}
$$

因此，若能将 $ H(j\omega) $ 展开成一些具有 (A.6) 式或 (A.8) 式这些项之和，就能凭直观求得

$ H(j\omega) $ 的反变换。例如，在 6.5.2 节中，注意到，当 $ c_1 \neq c_2 $ 时，(A.3) 式就可以重新写成如下形式：

$$
H(\mathrm{j}\omega)\;=\;\Big(\frac{\omega_{n}^{2}}{c_{1}-c_{2}}\Big)\frac{1}{\mathrm{j}\omega-c_{1}}+\Big(\frac{\omega_{n}^{2}}{c_{2}-c_{1}}\Big)\frac{1}{\mathrm{j}\omega-c_{2}}
$$

这时，就可以利用(A.5)式和(A.6)式的傅里叶变换对，立即写出 $ H(j\omega) $的反变换为

$$
h\left(t\right)=\left[\frac{\omega_{n}^{2}}{c_{1}-c_{2}}\mathrm{e}^{c_{1}t}+\frac{\omega_{n}^{2}}{c_{2}-c_{1}}\mathrm{e}^{c_{2}t}\right]u\left(t\right)
$$

虽然以上所讨论的是针对连续时间傅里叶变换的，但类似的概念对离散时间傅里叶分析和在拉普拉斯变换及z变换的应用中也同样适用。在所有这些情况中，尤其是遇到有理变换这样一类重要的类型，即变换式是某个变量的多项式之比时更是如此。同时，在每种情况下，都能发现为什么要将变换式展开成形如(A.9)式的这些简单项之和的原因。在这一节，为了导出求这种展开式的一般方法，现考虑一个一般变量v的有理函数，即考查具有如下形式的函数

$$
H(v)\;=\;\frac{\beta_{m}v^{m}+\beta_{m-1}v^{m-1}+\cdots+\beta_{1}v+\beta_{0}}{\alpha_{n}v^{n}+\alpha_{n-1}v^{n-1}+\cdots+\alpha_{1}v+\alpha_{0}}
$$

对于连续时间傅里叶分析来说，v 就相当于 $ (j\omega) $；而对拉普拉斯变换来说，v 就对应于复变量 $ s $。在离散时间傅里叶分析中，通常将 v 取作 $ e^{-j\omega} $；而对 z 变换，可用 $ z^{-1} $ 或者 z 取代 v。在导出部分分式展开的基本方法之后，再说明它在连续和离散时间 LTI 系统分析中的应用。

### A.2 部分分式展开和连续时间信号与系统 {#sec:A-2}

在推导中，为了方便起见，设有理函数是两种标准形式中的一种。其中第二种形式在离散时间信号与系统分析中是常用的，将给予简要讨论。第一种标准形式是

$$
G(v)=\frac{b_{n-1}v^{n-1}+b_{n-2}v^{n-2}+\cdots+b_{1}v+b_{0}}{v^{n}+a_{n-1}v^{n-1}+\cdots+a_{1}v+a_{0}}
$$

在这种形式中，分母中阶数最高的项的系数为1，并且分子的阶数低于分母的阶数（如 $ b_{n-1}=0 $，分子的阶数将低于n-1）。

如果以(A.11)式的形式给出 $ H(v) $，可以经由两步简单的计算得到形如(A.12)式的有理函数。第一步，将 $ H(v) $ 的分子分母同除以 $ \alpha_{n} $，得

$$
H(v)=\frac{\gamma_{m}v^{m}+\gamma_{m-1}v^{m-1}+\cdots+\gamma_{1}v+\gamma_{0}}{v^{n}+a_{n-1}v^{n-1}+\cdots+a_{1}v+a_{0}}
$$

这里

$$
\begin{array}{c c}{{\gamma_{m}=\frac{\beta_{m}}{\alpha_{n}},\quad}}&{{\gamma_{m-1}=\frac{\beta_{m-1}}{\alpha_{n}},\cdots}}\\ {{}}&{{}}\\ {{a_{n-1}=\frac{\alpha_{n-1}}{\alpha_{n}},\quad}}&{{a_{n-2}=\frac{\alpha_{n-2}}{\alpha_{n}},\cdots}}\end{array}
$$

如果 m<n, $ H(v) $ 称为严格真有理函数，在这种情况下，令 $ b_{0}=\gamma_{0} $, $ b_{1}=\gamma_{1} $, $ \cdots $, $ b_{m}=\gamma_{m} $，并置余下的 b 都等于零，(A.13)式中的 $ H(v) $ 就已经具有 (A.12) 式的形式了。本书大多

数情况有关有理函数的讨论主要都是关于严格真有理函数的。然而，如果 $ H(v) $ 不是真有理函数（即 $ m \geqslant n $），可以通过基本的计算，将 $ H(v) $ 写成一个 v 的多项式与一个严格真有理函数之和，即

$$
\begin{aligned}{H(v)=}&{{}\;c_{m-n}v^{m-n}+c_{m-n-1}v^{m-n-1}+\cdots+c_{1}v+c_{0}}\\ {}&{{}+\frac{b_{n-1}v^{n-1}+b_{n-2}v^{n-2}+\cdots+b_{1}v+b_{0}}{v^{n}+a_{n-1}v^{n-1}+\cdots+a_{1}v+a_{0}}}\\ \end{aligned}
$$

系数 $ c_{0} $, $ c_{1} $, $ \cdots $, $ c_{m-n} $ 和 $ b_{0} $, $ b_{1} $, $ \cdots $, $ b_{n-1} $ 可通过令(A.13)式和(A.14)式相等，然后两边同乘以分母而求得，即

$$
\begin{aligned}{\gamma_{m}v^{m}+\cdots+\gamma_{1}v+\gamma_{0}=}&{{}b_{n-1}v^{n-1}+\cdots+b_{1}v+b_{0}}\\ {}&{{}+\big(c_{m-n}v^{m-n}+\cdots+c_{0}\big)\big(v^{n}+a_{n-1}v^{n-1}+\cdots+a_{0}\big)}\\ \end{aligned}
$$

令(A.15)式两边 v 次幂相同的项系数相等，就能利用 a 和 $ \gamma $ 的值求得 c 和 b 的值。例如，若 m=2, n=1。则

$$
H(v)=\frac{\gamma_{2}v^{2}+\gamma_{1}v+\gamma_{0}}{v+a_{1}}=c_{1}v+c_{0}+\frac{b_{0}}{v+a_{1}}
$$

这时，(A.15)式就变成

$$
\begin{aligned}{\gamma_{2}v^{2}+\;\gamma_{1}v+\;\gamma_{0}}&{{}=b_{0}+\left(c_{1}v\;+\;c_{0}\right)\left(v\;+\;a_{1}\right)}\\ {}&{{}=b_{0}+c_{1}v^{2}+\left(c_{0}+a_{1}c_{1}\right)v\;+\;a_{1}c_{0}}\\ \end{aligned}
$$

由相同次幂项的系数相等，就得如下方程：

$$
\begin{aligned}\gamma_{2}&=c_{1}\\\gamma_{1}&=c_{0}+a_{1}c_{1}\\\gamma_{0}&=b_{0}+a_{1}c_{0}\end{aligned}
$$

从第一个方程直接得到 $ c_{1} $ 值，代入第二个方程可解得 $ c_{0} $，依次将 $ c_{0} $， $ c_{1} $ 代入第三个方程求得 $ b_{0} $，最后结果是

$$
\begin{aligned}{c_{1}}&{{}=\gamma_{2}}\\ {c_{0}}&{{}=\gamma_{1}-a_{1}\gamma_{2}}\\ {b_{0}}&{{}=\gamma_{0}-a_{1}(\gamma_{1}-a_{1}\gamma_{2})}\\ \end{aligned}
$$

(A.15)式的一般情况可用类似的方法来解。

现在，把目标放在(A.12)式的真有理函数 G(v)上，将它展开成简单的真有理函数之和。为了看清展开方法，考虑 n=3 的情况，这时(A.12)式简化成

$$
G(v)=\frac{b_{2}v^{2}+b_{1}v+b_{0}}{v^{3}+a_{2}v^{2}+a_{1}v+a_{0}}
$$

第一步先将 $ G(v) $ 的分母因式分解，为此将它写成

$$
G(v)=\frac{b_{2}v^{2}+b_{1}v+b_{0}}{(v-\rho_{1})(v-\rho_{2})(v-\rho_{3})}
$$

暂且假设分母的根 $ \rho_{1} $， $ \rho_{2} $ 和 $ \rho_{3} $ 都不相同，可将 $ G(v) $ 展开成如下形式的和：

$$
G(v)=\frac{A_{1}}{v-\rho_{1}}+\frac{A_{2}}{v-\rho_{2}}+\frac{A_{3}}{v-\rho_{3}}
$$

接下来就是确定系数 $ A_{1} $， $ A_{2} $ 和 $ A_{3} $。一种方法是令(A.18)式与(A.19)式相等，然后两边同

乘以分母。这种情况下，可得到方程

$$
\begin{aligned}{b_{2}v^{2}+b_{1}v+b_{0}=}&{{}A_{1}(v-\rho_{2})(v-\rho_{3})}\\ {}&{{}+A_{2}(v-\rho_{1})(v-\rho_{3})+A_{3}(v-\rho_{1})(v-\rho_{2})}\\ \end{aligned}
$$

将(A.20)式的右边展开，并令 v 的同幂次项的系数相等，可以得到一组线性方程，以解出 $ A_{1} $， $ A_{2} $ 和 $ A_{3} $。

虽然这种方法总是可行的，但还有一种更简单的方法。考虑(A.19)式，并假定要想计算 $ A_{1} $，那么两边都乘以 $ (v-\rho_{1}) $，得

$$
(v-\rho_{1})G(v)=A_{1}+\frac{A_{2}(v-\rho_{1})}{v-\rho_{2}}+\frac{A_{3}(v-\rho_{1})}{v-\rho_{3}}
$$

因为 $ \rho_{1} $， $ \rho_{2} $ 和 $ \rho_{3} $ 是各不相同的，对于 $ v=\rho_{1} $，(A.21) 式右边的最后两项等于零，因此

$$
A_{1}=\left[\left(v-\rho_{1}\right)G(v)\right]\mid_{v=\rho_{1}}
$$

或者，利用(A.18)式

$$
A_{1}=\frac{b_{2}\rho_{1}^{2}+b_{1}\rho_{1}+b_{0}}{(\rho_{1}-\rho_{2})(\rho_{1}-\rho_{3})}
$$

同理

$$
A_{2}=\left[\left(v-\rho_{2}\right)G(v)\right]\mid_{v=\rho_{2}}=\frac{b_{2}\rho_{2}^{2}+b_{1}\rho_{2}+b_{0}}{\left(\rho_{2}-\rho_{1}\right)\left(\rho_{2}-\rho_{3}\right)}
$$

$$
A_{3}=\left[\left(v-\rho_{3}\right)G(v)\right]\mid_{v=\rho_{3}}=\frac{b_{2}\rho_{3}^{2}+b_{1}\rho_{3}+b_{0}}{\left(\rho_{3}-\rho_{1}\right)\left(\rho_{3}-\rho_{2}\right)}
$$

现在假设 $ \rho_{1}=\rho_{3}\neq\rho_{2} $，即

$$
G(v)=\frac{b_{2}v^{2}+b_{1}v+b_{0}}{(v-\rho_{1})^{2}(v-\rho_{2})}
$$

在这种情况下，要寻求一种

$$
G(v)=\frac{A_{11}}{v-\rho_{1}}+\frac{A_{12}}{(v-\rho_{1})^{2}}+\frac{A_{21}}{v-\rho_{2}}
$$

的展开式。这里，当把(A.27)式通分时，为了得到正确的分母，就需要有 $ 1/(v-\rho_{1})^{2} $这一项。在一般情况下，也需要包括 $ 1/(v-\rho_{1}) $这一项。为了说明其理由，考虑令(A.26)式和(A.27)式相等，两边再同乘以(A.26)式的分母，得

$$
b_{2}v^{2}+b_{1}v+b_{0}=A_{11}(v-\rho_{1})(v-\rho_{2})+A_{12}(v-\rho_{2})+A_{21}(v-\rho_{1})^{2}
$$

如果再次令相同次幂项的系数相等，就得到三个方程（对于 $ v^{0} $， $ v^{1} $ 和 $ v^{2} $ 项的系数）。倘若略去（A.27）式中的 $ A_{11} $ 项，将得到含有两个未知量的三个方程；这样，一般将不是一个解。一旦包括了这一项，总是能求得一个解。然而，在这种情况下，还有一个更简单的方法。考虑 (A.27) 式，两边同乘以 $ (v - \rho_{1})^{2} $：

$$
(v-\rho_{1})^{2}G(v)=A_{11}(v-\rho_{1})+A_{12}+\frac{A_{21}(v-\rho_{1})^{2}}{v-\rho_{2}}
$$

从上面的例子，可立即看出如何来确定 $ A_{12} $:

$$
A_{12}=\left[\left(\upsilon-\rho_{1}\right)^{2}G(\upsilon)\right]\mid_{\upsilon=\rho_{1}}=\frac{b_{2}\rho_{1}^{2}+b_{1}\rho_{1}+b_{0}}{\rho_{1}-\rho_{2}}
$$

至于 $ A_{11} $，假设将 $ (\Lambda,29) $式两边对v微分：

$$
\frac{\mathrm{d}}{\mathrm{d}v}[(\upsilon-\rho_{1})^{2}G(\upsilon)]=A_{11}+A_{21}\bigg[\frac{2(\upsilon-\rho_{1})}{\upsilon-\rho_{2}}-\frac{(\upsilon-\rho_{1})^{2}}{(\upsilon-\rho_{2})^{2}}\bigg]
$$

这时很明显，对于 $ v=\rho_{1} $，(A.31) 式中最后一项是零，因此

$$
\begin{aligned}\Lambda_{11}=&\left[\frac{\mathrm{d}}{\mathrm{d}v}(v-\rho_{1})^{2}G(v)\right]\bigg|_{v=\rho_{1}}\\ =&\frac{2b_{2}\rho_{1}+b_{1}}{\rho_{1}-\rho_{2}}-\frac{b_{2}\rho_{1}^{2}+b_{1}\rho_{1}+b_{0}}{(\rho_{1}-\rho_{2})^{2}}\end{aligned}
$$

最后，把(A.27)式乘以 $ (v-\rho_{2}) $，可以求得

$$
A_{21}=\lceil\left(v-\rho_{2}\right)G\left(v\right)\rceil\mid_{v=\rho_{2}}=\frac{b_{2}\rho_{2}^{2}+b_{1}\rho_{2}+b_{0}}{(\rho_{2}-\rho_{1})^{2}}
$$

这个例子说明了在一般情况下，部分分式展开中的所有基本概念。特别是，设(A.12)式中 $ G(v) $ 的分母有不同的根 $ \rho_{1}, \cdots, \rho_{r} $ 分别具有 $ \sigma_{1}, \cdots, \sigma_{r} $ 重根时，那么

$$
G(v)\simeq\frac{b_{n-1}v^{n-1}+\cdots+b_{1}v+b_{0}}{(v-\rho_{1})^{\sigma_{1}}(v-\rho_{2})^{\sigma_{2}}\cdots(v-\rho_{r})^{\sigma_{r}}}
$$

这时， $ G(v) $ 具有部分分式展开的形式为

$$
\begin{aligned}{G\left(v\right)}&{{}=\frac{A_{11}}{v-\rho_{1}}+\frac{A_{12}}{\left(v-\rho_{1}\right)^{2}}+\cdots+\frac{A_{1\sigma_{1}}}{\left(v-\rho_{1}\right)^{\sigma_{1}}}+\frac{A_{21}}{v-\rho_{2}}}\\ {}&{{}\quad+\cdots+\frac{A_{2\sigma_{2}}}{\left(v-\rho_{2}\right)^{\sigma_{2}}}+\cdots+\frac{A_{r1}}{v-\rho_{r}}+\cdots+\cdots+\frac{A_{r\sigma_{r}}}{\left(v-\rho_{r}\right)^{\sigma_{r}}}}\\ {}&{{}=\sum_{i=1}^{r}\sum_{k=1}^{\sigma_{i}}\frac{A_{i k}}{\left(v-\rho_{i}\right)^{k}}}\\ \end{aligned}
$$

的展开式，这里 $ A_{ik} $由下式 $ ^{①} $计算出：

$$
A_{i k}=\frac{1}{(\sigma_{i}-k)!}\bigg[\frac{d^{\sigma_{i}-k}}{d v^{\sigma_{i}-k}}\big[\left(v-\rho_{i}\right)^{\sigma_{i}}G(v)\big]\bigg]\bigg|_{v=\rho_{i}}
$$

这个结果可以用象上面例子一样来校验：将(A.35)式两边乘以 $ (v-\rho_{i})^{\sigma_{i}} $，并重复求导，直到 $ A_{ik} $不再乘有 $ (v-\rho_{i}) $的次幂为止，然后令 $ v=\rho_{i} $。

例 A.1 在例 4.25 中，研究了一个由微分方程

$$
\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}+4\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+3y\left(t\right)=\frac{\mathrm{d}x\left(t\right)}{\mathrm{d}t}+2x\left(t\right)
$$

描述的 LTI 系统。该系统的频率响应是

$$
H(\mathrm{j}\omega)=\frac{\mathrm{j}\omega+2}{(\mathrm{j}\omega)^{2}+4\mathrm{j}\omega+3}
$$

为了确定这个系统的单位冲激响应，将 $ H(j\omega) $ 展开成一些简单项的和，而这些简单项的反变换凭直观就能求得。将 $ j\omega $ 换成 v，就得到下面函数：

$$
G(v)=\frac{v+2}{v^{2}+4v+3}=\frac{v+2}{(v+1)(v+3)}
$$

$ G(v) $的部分分式展开是

$$
G(v)=\frac{A_{11}}{v+1}+\frac{A_{21}}{v+3}
$$

其中

$$
A_{11}=\left[\left(v+1\right)G(v)\right]|_{v=-1}=\frac{-1+2}{-1+3}=\frac{1}{2}
$$

$$
A_{21}=\left[\left(v+3\right)G(v)\right]\mid_{v=-3}=\frac{-3+2}{-3+1}=\frac{1}{2}
$$

于是

$$
H(\mathrm{j}\omega)=\frac{\frac{1}{2}}{\mathrm{j}\omega+1}+\frac{\frac{1}{2}}{\mathrm{j}\omega+3}
$$

将(A.43)式取反变换，就得该系统的单位冲激响应

$$
h\left(t\right)=\frac{1}{2}\mathrm{e}^{-1}u\left(t\right)+\frac{1}{2}\mathrm{e}^{-3t}u\left(t\right)
$$

由(A.37)式描述的系统也能用拉普拉斯变换分析方法来分析，该系统的系统函数是

$$
H(s)=\frac{s+2}{s^{2}+4s+3}
$$

并且，若以 v 代替 s，就得到如(A.39)式相同的 G(v)。因此，其部分分式展开完全与(A.40)式到(A.42)式相同，其结果是

$$
H(s)\;=\;{\frac{{\frac{1}{2}}}{s+1}}+{\frac{{\frac{1}{2}}}{s+3}}
$$

求该式的反变换就得到单位冲激响应，如(A.44)式所给出。

例 A.2 现在说明当分母中具有重因子时部分分式展开的方法。在例 4.26 中考虑过当输入为

$$
x(t)=\mathrm{e}^{-t}u(t)
$$

时，由(A.37)式描述的系统响应。由(4.81)式，系统输出的傅里叶变换是

$$
Y(\mathrm{j}\omega)=\frac{\mathrm{j}\omega+2}{(\mathrm{j}\omega+1)^{2}(\mathrm{j}\omega+3)}
$$

以 v 代替 jω，就得有理函数

$$
G(v)=\frac{v+2}{(v+1)^{2}(v+3)}
$$

这个函数的部分分式展开是

$$
G(v)=\frac{A_{11}}{v+1}+\frac{A_{12}}{(v+1)^{2}}+\frac{A_{21}}{v+3}
$$

其中，由(A.36)式

$$
A_{11}=\frac{1}{(2-1)!}\;\frac{\mathrm{d}}{\mathrm{d}v}\big[(\mathbf{\nabla}v+1)^{2}G(\mathbf{\nabla}v)\big]\mid_{v=-1}=\frac{1}{4}
$$

$$
A_{12}=\left[(v+1)^{2}G(v)\right]\mid_{v=-1}=\frac{1}{2}
$$

$$
A_{21}=\left[\left(v+3\right)G(v)\right]\mid_{v=-3}=-\frac{1}{4}
$$

因此

$$
Y(\mathrm{j}\omega)=\frac{\frac{1}{4}}{\mathrm{j}\omega+1}+\frac{\frac{1}{2}}{(\mathrm{j}\omega+1)^{2}}-\frac{\frac{1}{4}}{\mathrm{j}\omega+3}
$$

取反变换就得到

$$
y(t)=\left[\frac{1}{4}\mathrm{e}^{-t}+\frac{1}{2}t\mathrm{e}^{-t}-\frac{1}{4}\mathrm{e}^{-3t}\right]u(t)
$$

同样，这个分析本来也能够用拉普拉斯变换来完成，并且所得代数表示式与(A.49)式到(A.55)式完全相同。

### A.3 部分分式展开和离散时间信号与系统 {#sec:A-3}

如前面提及的，在对离散时间傅里叶变换或z变换式实行部分分式展开时，另一种形式稍有不同的有理函数形式常常更便于处理。现假设有一个有理函数，其形式为

$$
G(v)=\frac{d_{n-1}v^{n-1}+\cdots+d_{1}v+d_{0}}{f_{n}v^{n}+\cdots+f_{1}v+1}
$$

这种形式的 $ G(v) $，可通过把(A.12)式中的 $ G(v) $ 分子分母同除以 $ a_{0} $ 而得到。

对于(A.56)式中给出的 $ G(v) $，分母相应的因式分解具有如下形式：

$$
G(v)=\frac{\mathrm{d}_{n-1}v^{n-1}+\cdots+\mathrm{d}_{1}v+d_{0}}{(1-\rho_{1}^{-1}v)^{\sigma_{1}}(1-\rho_{2}^{-1}v)^{\sigma_{2}\cdots}(1-\rho_{r}^{-1}v)^{\sigma_{r}}}
$$

部分分式展开的形式为

$$
G(v)=\sum_{i=1}^{r}\sum_{k=1}^{\sigma_{i}}\frac{B_{ik}}{(1-\rho_{i}^{-1}v)^{k}}
$$

$ B_{ik} $ 可用类似于前面使用过的方法计算得

$$
B_{i k}=\frac{1}{(\sigma_{i}-k)!}(-\rho_{i})^{\sigma_{i}-k}\left[\frac{\mathrm{d}^{\sigma_{i}-k}}{\mathrm{d}v^{\sigma_{i}-k}}\left[(1-\rho_{i}^{-1}v)^{\sigma_{i}}G(v)\right]\right]|_{v=\rho_{i}}
$$

同前面一样，(A.59)式的正确性可以这样验证：将(A.58)式两边各乘以 $ (1-\rho_{i}^{-1}v)^{\sigma_{i}} $，然后重复对v求导，直到 $ B_{ik} $中不再有乘以 $ (1-\rho_{i}^{-1}v) $的幂为止，最后令 $ v=\rho_{i} $

$$
y[n]-\frac{3}{4}y[n-1]+\frac{1}{8}y[n-2]=2x[n]
$$

例 A.3 考虑在例 5.19 的因果 LT1 系统，其差分方程为

该系统的频率响应是

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{2}{1-\frac{3}{4}\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{8}\mathrm{e}^{-2\mathrm{j}\omega}}
$$

对于像这样的离散时间变换，最方便地是用 v 来代替 $ e^{-j\omega} $。作这样的替换后，得到有理函数为

$$
G(v)=\frac{2}{1-\frac{3}{4}v+\frac{1}{8}v^{2}}=\frac{2}{(1-\frac{1}{2}v)(1-\frac{1}{4}v)}
$$

利用由(A.57)式到(A.59)式给出的部分分式展开式，得到

$$
G(v)=\frac{B_{11}}{1-\frac{1}{2}v}+\frac{B_{21}}{1-\frac{1}{4}v}
$$

$$
B_{\mathrm{i1}}=\left[\left(1-\frac{1}{2}v\right)G(v)\right]\bigg|_{v=2}=\frac{2}{1-\frac{1}{2}}=4
$$

$$
B_{21}=\left[\left(1-\frac{1}{4}v\right)G(v)\right]\bigg|_{v=4}=\frac{2}{1-2}=-2
$$

于是有

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{4}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}-\frac{2}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}},
$$

将(A.66)式取反变换，得到单位脉冲响应为

$$
h[n]=4\Bigl(\frac{1}{2}\Bigr)^{n}u[n]-2\Bigl(\frac{1}{4}\Bigr)^{n}u[n].
$$

在10.7节，提出了用z变换分析方法对由线性常系数差分方程表征的离散时间LTI系统进行研究。把这个分析方法应用于这个例子，发现该系统函数可由(A.60)式凭直观可以确定是

$$
H(z)=\frac{2}{1-\frac{3}{4}z^{-1}+\frac{1}{8}z^{-2}}
$$

然后，用 v 代替 $ z^{-1} $，就得出如(A.62)式的 $ G(v) $，利用(A.63)式到(A.65)式的部分分式展开式计算，求得

$$
H(z)=\frac{4}{1-\frac{1}{2}z^{-1}}-\frac{2}{1-\frac{1}{4}z^{-1}}
$$

当反变换后，就得到(A.67)式的单位脉冲响应。

**例 A.4 假定例 A.3 考虑的系统输入是**

$$
x[n]=\left(\frac{1}{4}\right)^{n} u[n]
$$

那么，由例5.20，输出的傅里叶变换是

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\frac{2}{(1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega})(1-\frac{1}{4}e^{-\mathrm{j}\omega})^{2}}
$$

用 v 代替 $ e^{-j\omega} $ 可得

$$
G(v)=\frac{2}{(1-\frac{1}{2}v)(1-\frac{1}{4}v)^{2}}
$$

于是，应用(A.58)式和(A.59)式，可得部分分式展开式为

$$
G(v)=\frac{B_{11}}{1-\frac{1}{4}v}+\frac{B_{12}}{(1-\frac{1}{4}v)^{2}}+\frac{B_{21}}{1-\frac{1}{2}v}
$$

并求得

$$
B_{11}=(-4)\bigg[\frac{\mathrm{d}}{\mathrm{d}v}\bigg(1-\frac{1}{4}v\bigg)^{2}G(v)\bigg]\bigg|_{v=4}=-4
$$

$$
B_{12}=\left.\left[\left(1-\frac{1}{4}v\right)^{2}G(v)\right]\right|_{v=4}=-2
$$

$$
B_{21}=\left.\left[\left(1-\frac{1}{2}v\right)G(v)\right]\right|_{v=2}=8
$$

因此

$$
Y(\mathrm{j}\omega)=-\frac{4}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}-\frac{2}{(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})^{2}}+\frac{8}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}
$$

利用表4.2的傅里叶变换时，凭直观就可求出反变换为：

$$
y[n]=\left\{-4\Big(\frac{1}{4}\Big)^{n}-2(n+1)\Big(\frac{1}{4}\Big)^{n}+8\Big(\frac{1}{2}\Big)^{n}\Big\}u[n]
$$

例 A.5 在离散时间系统分析中，常常碰到假有理函数。为了说明这个问题，同时也指出如何用在本附录中提出的方法进行分析，考虑由差分方程

$$
y[n]+\frac{5}{6}y[n-1]+\frac{1}{6}y[n-2]=x[n]+3x[n-1]+\frac{11}{6}x[n-2]+\frac{1}{3}x[n-3]
$$

表征的因果 LTI 系统。该系统的频率响应是

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{1+3\mathrm{e}^{-\mathrm{j}\omega}+\frac{11}{6}\mathrm{e}^{-\mathrm{j}2\omega}+\frac{1}{3}\mathrm{e}^{-\mathrm{j}3\omega}}{1+\frac{5}{6}\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{6}\mathrm{e}^{-\mathrm{j}2\omega}}
$$

用 v 代替 $ e^{-j\omega} $ 可得

$$
G(v)\;=\;{\frac{1+3v+{\frac{11}{6}}v^{2}+{\frac{1}{3}}v^{3}}{1+{\frac{5}{6}}v+{\frac{1}{6}}v^{2}}}
$$

这个有理函数可以写成一个多项式和一个真有理函数之和：

$$
G(v)=c_{0}+c_{1}v+\frac{b_{1}v+b_{0}}{1+\frac{5}{6}v+\frac{1}{6}v^{2}}
$$

令(A.80)式和(A.81)式相等，并乘以 $ (1+\frac{5}{6}v+\frac{1}{6}v^{2}) $，得

$$
\begin{aligned}1+3v+\frac{11}{6}v^{2}+\frac{1}{3}v^{3}=&\left(c_{0}+b_{0}\right)+\left(\frac{5}{6}c_{0}+c_{1}+b_{1}\right)v\\&+\left(\frac{1}{6}c_{0}+\frac{5}{6}c_{1}\right)v^{2}+\frac{1}{6}c_{1}v^{3}\end{aligned}
$$

令各系数相等，可得

$$
\begin{aligned}&\frac{1}{6}c_{1}=\frac{1}{3}\rightarrow c_{1}=2\\&\frac{1}{6}c_{0}+\frac{5}{6}c_{1}=\frac{11}{6}\rightarrow c_{0}=1\\&\frac{5}{6}c_{0}+c_{1}+b_{1}=3\rightarrow b_{1}=\frac{1}{6}.\\&c_{0}+b_{0}=1\rightarrow b_{0}=0\end{aligned}
$$

因此

$$
H(\mathrm{e}^{\mathrm{j}\omega})=1+2\mathrm{e}^{-\mathrm{j}\omega}+\frac{\frac{1}{6}\mathrm{e}^{-\mathrm{j}\omega}}{1+\frac{5}{6}\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{6}\mathrm{e}^{-\mathrm{j}2\omega}}
$$

另外，采用本附录提出的方法，将(A.81)式中的真有理函数展开成

$$
\frac{\frac{1}{6}v}{1+\frac{5}{6}v+\frac{1}{6}v^{2}}=\frac{\frac{1}{6}v}{(1+\frac{1}{3}v)(1+\frac{1}{2}v)}=\frac{B_{11}}{(1+\frac{1}{3}v)}+\frac{B_{21}}{(1+\frac{1}{2}v)}
$$

这些系数是

$$
B_{11}=\left.\left(\frac{\frac{1}{6}v}{1+\frac{1}{2}v}\right)\right|_{v=-3}=1
$$

$$
B_{21}=\left.\left(\frac{\frac{1}{6}v}{1+\frac{1}{3}v}\right)\right|_{v=-2}=-1
$$

因此求得

$$
H(\mathrm{e}^{\mathrm{j}\omega})=1+2\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{1+\frac{1}{3}\mathrm{e}^{-\mathrm{j}\omega}}-\frac{1}{1+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}
$$

凭直观可求得该系统的单位脉冲响应为

$$
h\left[n\right]=\delta\left[n\right]+2\delta\left[n-1\right]+\left[\left(-\frac{1}{3}\right)^{n}-\left(-\frac{1}{2}\right)^{n}\right]u\left[n\right]
$$
