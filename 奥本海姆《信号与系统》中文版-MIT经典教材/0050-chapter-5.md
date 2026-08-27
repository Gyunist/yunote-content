## 第5章 离散时间傅里叶变换 {#sec:5}

### 5.0 引言 {#sec:5-0}

第4章我们研究了连续时间傅里叶变换，并研究了这种变换的许多特性，这些特性使傅里叶分析方法在分析和理解连续时间信号与系统的性质中具有很大的价值。这一章将介绍并研究离散时间傅里叶变换，这样就完整地建立了傅里叶分析方法。

在第3章讨论傅里叶级数时，曾看到在连续时间和离散时间信号分析中存在着很多相类似的地方，并且在分析途径上也是并行的；然而，也有一些重大的差别。例如，在3.6节，离散时间周期信号的傅里叶级数表示是一个有限项级数；而连续时间周期信号则要求一个无穷项级数的表示。这一章将会看到，连续时间和离散时间傅里叶变换之间也存在着相应的差别。

这一章将基本上与第4章所采用的办法相同，即充分利用连续时间和离散时间傅里叶分析之间的类似性来展开讨论。这就是，首先为了建立离散时间非周期信号的傅里叶变换表示，而将周期信号的傅里叶级数表示进行推广，接着采用与第4章相平行地做法，分析离散时间傅里叶变换的性质和特点。这样做不仅加深了对连续时间和离散时间所共有的傅里叶分析基本概念的理解，而且还对比了它们之间的差别，以更加突出对它们各自独特性质的理解。

### 5.1 非周期信号的表示：离散时间傅里叶变换 {#sec:5-1}

#### 5.1.1 离散时间傅里叶变换的导出 {#sec:5-1-1}

在4.1节[(4.2)式和图4.2]曾经看到，一个连续时间周期方波的傅里叶级数可以看作是一个包络函数的采样值，并且随着这个方波周期的增大，这些样本变得愈来愈密。这一性质就使人想到一个非周期信号 $ x(t) $可以这样来表示，即：首先做一个周期信号 $ \tilde{x}(t) $，使得 $ \tilde{x}(t) $在一个周期内等于 $ x(t) $，然后随着这个周期趋于无限大， $ \tilde{x}(t) $就会在一个愈来愈大的时间间隔上等于 $ x(t) $，这样对 $ \tilde{x}(t) $的傅里叶级数表示也就收敛于 $ x(t) $的傅里叶变换表示。在这一节，对离散时间非周期序列，为了建立它的傅里叶变换表示，将采用与在连续时间情况下完全类似的步骤进行。

考虑某一序列 $ x[n] $，它具有有限持续期；也就是说，对于某个整数 $ N_{1} $ 和 $ N_{2} $，在 $ -N_{1} \leqslant n \leqslant N_{2} $ 以外， $ x[n] = 0 $。图 5.1(a) 示出这种类型的一个信号。由这个非周期信号可以构成一个周期序列 $ \tilde{x}[n] $，使得对 $ \tilde{x}[n] $ 来说 $ x[n] $ 是它的一个周期，如图 5.1(b) 所示。随着所选周期 N 的增大， $ \tilde{x}[n] $ 就在一个更长的时间间隔内与 $ x[n] $ 一样，而当 $ N \to \infty $ 时，对任意有限 n 值来说，有 $ \tilde{x}[n] = x[n] $。

现在来考查一下 $ \tilde{x}[n] $的傅里叶级数表示式。由(3.94)式和(3.95)式，有

![图像（物理页 279，第 1 幅）](../Figures/fig-p0279-01.jpg){#fig:p279-1}

**(a)**

**(b)**

**图 5.1 (a) 有限长序列 x[n]; (b) 由 x[n] 构成的周期序列 $ \tilde{x}[n] $**

$$
\bar{x}[n]=\sum_{k=(N)}a_{k}\mathrm{e}^{\mathrm{j}k(2\pi/N)n}
$$

$$
a_{k}=\frac{1}{N}\sum_{n=(N)}\tilde{x}\left[n\right]\mathrm{e}^{-\mathrm{j}k\left(2\pi/N\right)n}
$$

因为在包括 $ -N_{1}\leqslant n\leqslant N_{2} $区间的一个周期上 $ x[n]=\tilde{x}[n] $，因此在(5.2)式中，求和区间就选在这个周期上，这样在(5.2)式的求和中就可用 $ x[n] $来代替 $ \tilde{x}[n] $，而得到

$$
a_{k}=\frac{1}{N}\sum_{n=-N_{1}}^{N_{2}}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n}=\frac{1}{N}\sum_{n=-\infty}^{+\infty}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n}
$$

上式中已经考虑到在 $ -N_{1} \leqslant n \leqslant N_{2} $ 以外， $ x[n] = 0 $ 这一点。现定义函数

$$
X(e^{j\omega})=\sum_{n=-\infty}^{+\infty}x[n]e^{-j\omega n}
$$

可见这些系数 $ a_{k} $ 是正比于 $ X(e^{j\omega}) $ 的各样本值，即

$$
a_{k}=\frac{1}{N}X(e^{j k\omega_{0}})
$$

式中 $ \omega_{0}=2\pi/N $ 用来记作在频域中的样本间隔。将(5.1)式和(5.5)式组合在一起后得

$$
\tilde{x}\left[n\right]=\sum_{k=(N)}\frac{1}{N}X(\mathrm{e}^{\mathrm{j}k\omega_{0}})\mathrm{e}^{\mathrm{j}k\omega_{0}n}
$$

因为 $ \omega_{0}=2\pi/N $ ，或 $ 1/N=\omega_{0}/2\pi $ ，所以(5.6)式又可写成

$$
\bar{x}[n]=\frac{1}{2\pi}\sum_{k=(N)}X(\mathrm{e}^{\mathrm{j}k\omega_{0}})\mathrm{e}^{\mathrm{j}k\omega_{0}n}\omega_{0}
$$

和(4.7)式相同，随着N增加， $ \omega_{0} $减小，一旦 $ N\to\infty $，(5.7)式就过渡为一个积分。为了更清楚地看到这点，把 $ X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega} $画在图5.2中。根据(5.4)式， $ X(\mathrm{e}^{\mathrm{j}\omega}) $对 $ \omega $来说是周期的，周期为 $ 2\pi $；而 $ \mathrm{e}^{\mathrm{j}\omega} $对 $ \omega $也是以 $ 2\pi $为周期的。所以乘积 $ X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega} $也一定是周期的。如图中所指出的，在(5.7)式求和中的每一项都代表了一个高为 $ X(\mathrm{e}^{\mathrm{j}\omega_{0}})\mathrm{e}^{\mathrm{j}\omega_{0}} $，宽为 $ \omega_{0} $的矩形面积。当 $ \omega_{0}\to0 $时，这个求和式就演变为一个积分。再说，因为这个求和是在N个宽为 $ \omega_{0}=2\pi/N $的

![图像（物理页 280，第 1 幅）](../Figures/fig-p0280-01.jpg){#fig:p280-1}

**图 5.2 (5.7) 式的图解说明**

间隔内完成的，所以总的积分区间总是有一个 $ 2\pi $ 的宽度。因此，随着 $ N \to \infty $， $ \tilde{x}[n] = x[n] $，(5.7)式就变成

$$
x[n]=\frac{1}{2\pi}\int_{2\pi}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega
$$

其中，因为 $ X(e^{j\omega})e^{j\omega m} $ 是周期的，周期为 $ 2\pi $，因此积分区间可以取任何长度为 $ 2\pi $ 的间隔。这样，就得到一对公式：

$$
x[n]=\frac{1}{2\pi}\int_{2\pi}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega m}\mathrm{d}\omega
$$

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{m=-\infty}^{+\infty}x[n]\mathrm{e}^{-\mathrm{j}m n}
$$

(5.8)式和(5.9)式是(4.8)式和(4.9)式在离散时间情况下所对应的关系。 $ X(e^{\mathrm{j}\omega}) $称为离散时间傅里叶变换，这一对式子就是离散时间傅里叶变换对。(5.8)式是综合公式，而(5.9)式则是分析公式。在推导这些公式的过程中表明一个非周期序列是如何能被看作复指数信号的线性组合的。事实上，综合公式本身就是把序列 $ x[n] $作为一种复指数序列的线性组合来表示的，这些复指数序列在频率上是无限靠近的，它们的幅度是 $ X(e^{\mathrm{j}\omega}) $（ $ \mathrm{d}\omega/2\pi $）。为此，像在连续时间情况一样，傅里叶变换 $ X(e^{\mathrm{j}\omega}) $往往被称为 $ x[n] $的频谱，因为它给出了这样的信息，就是 $ x[n] $是怎样由这些不同频率的复指数序列组成的。

值得提及的是，与连续时间情况一样，上述离散时间傅里叶变换的推导过程给我们在离散时间傅里叶级数和离散时间傅里叶变换之间提供了一种重要的关系。这就是，一个周期信号 $ \tilde{x}[n] $ 的傅里叶系数 $ a_k $ 可以用一个有限长序列 $ x[n] $ 的傅里叶变换的等间隔样本来表示，这个 $ x[n] $ 就等于在一个周期上的 $ \tilde{x}[n] $，而在其余地方为零。这一点在实际的信号处理和傅里叶分析中极为重要，在习题 5.41 中将进一步给予讨论。

正如在推导过程中所表明的，离散时间傅里叶变换和连续时间情况相比具有许多类似之处。两者的主要差别在于离散时间变换 $ X(e^{j\omega}) $ 的周期性和在综合公式中的有限积分区间。这两者均来自这样一个事实（以前已经多次提到）：在频率上相差 $ 2\pi $ 的离散时间复指数信号是完全一样的。在 3.6 节已看到，对周期离散时间信号而言，这就意味着傅里叶级数系数也是周期的，以及傅里叶级数表示式是一个有限项的和式。对非周期信号而言，这就意味着 $ X(e^{j\omega}) $ 也是周期的（周期为 $ 2\pi $），以及综合公式只涉及到在一个频率区间内的积分，这个频率

区间就是产生不同复指数信号的那个间隔，即任何 $ 2\pi $ 长度的间隔。在 1.3.3 节曾指出过 $ e^{j\omega t} $ 作为 $ \omega $ 函数的周期性的进一步结果是： $ \omega = 0 $ 和 $ \omega = 2\pi $ 都得出同一个信号。因此，位于这些频率值或任何 $ \pi $ 偶数倍的 $ \omega $ 附近都是慢变化的，从而都相应于低频率的信号；而靠近 $ \pi $ 的奇数倍的 $ \omega $，在离散时间情况下都相应于高的频率。因此，在图 5.3(a) 中的信号[其傅里叶变换画在图 5.3(b) 上]其变化比图 5.3(c) 的信号[其变换如图 5.3(d) 所示]要更慢一些。

![图像（物理页 281，第 1 幅）](../Figures/fig-p0281-01.jpg){#fig:p281-1}

**(a)**

![图像（物理页 281，第 2 幅）](../Figures/fig-p0281-02.jpg){#fig:p281-2}

**(b)**

![图像（物理页 281，第 3 幅）](../Figures/fig-p0281-03.jpg){#fig:p281-3}

**(c)**

![图像（物理页 281，第 4 幅）](../Figures/fig-p0281-04.jpg){#fig:p281-4}

**(d)**

**图5.3 (a)离散时间信号 $ x_{1}[n] $; (b) $ x_{1}[n] $ 的傅里叶变换 [注意: $ X_{1}(e^{j\omega}) $ 是集中在 $ \omega = 0 $, $ \pm 2\pi $, $ \pm 4\pi $, …附近]; (c) 离散时间信号 $ x_{2}[n] $; (d) $ x_{2}[n] $ 的傅里叶变换 [注意: $ X_{2}(e^{j\omega}) $ 是集中在 $ \omega = \pm \pi $, $ \pm 3\pi $, …附近]**

#### 5.1.2 离散时间傅里叶变换举例 {#sec:5-1-2}

为了说明离散时间傅里叶变换，考虑下面几个例子。

**例5.1 考虑信号**

$$
x[n]=a^{n} u[n],\qquad|\textit{a}|<1
$$

这时

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}a^{n}u[n]\mathrm{e}^{-\mathrm{j}\omega n}=\sum_{n=0}^{\infty}(a\mathrm{e}^{-\mathrm{j}\omega})^{n}=\frac{1}{1-a\mathrm{e}^{-\mathrm{j}\omega}}
$$

图5.4(a)示出了a>0时， $ X(e^{j\omega}) $的模和相位；图5.4(b)示出a<0时的模和相位。应该注意，图中所有这些函数都是周期为 $ 2\pi $的周期函数。

$$
x[n]=a^{|n|},\quad|\alpha|<1
$$

**例5.2 设**

![图像（物理页 282，第 1 幅）](../Figures/fig-p0282-01.jpg){#fig:p282-1}

**图 5.4 例 5.1 傅里叶变换的模和相位: (a) a>0; (b) a<0**

该信号对于 0 < a < 1 如图 5.5(a) 所示。它的傅里叶变换由 (5.9) 式可求出为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}a^{\mathrm{i}\pi\mathrm{i}}\mathrm{e}^{-\mathrm{j}\omega n}=\sum_{n=0}^{\infty}a^{n}\mathrm{e}^{-\mathrm{j}\omega n}+\sum_{n=-\infty}^{-1}a^{-n}\mathrm{e}^{-\mathrm{j}\omega n}
$$

在上式第二个求和式中，以 m = -n 置换，可得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=0}^{\infty}(a\mathrm{e}^{-\mathrm{j}\omega})^{n}+\sum_{m=1}^{\infty}(a\mathrm{e}^{\mathrm{j}\omega})^{m}
$$

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}+\frac{\alpha\mathrm{e}^{\mathrm{j}\omega}}{1-\alpha\mathrm{e}^{\mathrm{j}\omega}}=\frac{1-a^{2}}{1-2a\cos\omega+a^{2}}
$$

这两个求和式都是无穷几何级数，可以用闭式表示为

在此情况下， $ X(e^{j\omega}) $ 是实函数，对于 0<a<1，如图 5.5(b) 所示。

![图像（物理页 283，第 1 幅）](../Figures/fig-p0283-01.jpg){#fig:p283-1}

![图像（物理页 283，第 2 幅）](../Figures/fig-p0283-02.jpg){#fig:p283-2}

**图5.5 (a) 例5.2中的信号 $ x[n]=a^{|x|} $; (b) 它的傅里叶变换 $ (0<a<1) $**

**例5.3 考虑下列矩形脉冲序列**

$$
x[n]=\left\{\begin{aligned}&1,~|~n|\leqslant N_{1}\\ &0,~|~n|>N_{1}\end{aligned}\right.
$$

图5.6(a)示出 $ N_{1}=2 $的x[n]，这时

利用在例3.12中求(3.104)式时使用过的类似计算，可得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-N_{1}}^{N_{1}}\mathrm{e}^{-\mathrm{j}\omega n}
$$

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{\sin\omega\left(N_{1}+\frac{1}{2}\right)}{\sin(\omega/2)}
$$

![图像（物理页 283，第 3 幅）](../Figures/fig-p0283-03.jpg){#fig:p283-3}

**(a)**

![图像（物理页 283，第 4 幅）](../Figures/fig-p0283-04.jpg){#fig:p283-4}

**图 5.6 (a) 例 5.3 在 $ N_{1}=2 $ 时的矩形脉冲序列；**

**(b) 对应的傅里叶变换**

对于 $ N_{1}=2 $ 的 $ X(e^{j\omega}) $ 如图 5.6(b) 所示。

(5.12)式的函数是 $ \sin c $函数在离散时间情况下所对应的形式(见例4.4)。这两个函数之间最重要的差别就是(5.12)式的函数是周期的，周期为 $ 2\pi $，而 $ \sin c $函数是非周期的。

#### 5.1.3 关于离散时间傅里叶变换的收敛问题 {#sec:5-1-3}

尽管以上讨论都是假设 $ x[n] $ 是任意的，但属有限长情况下得到的结论，但是(5.8)式和(5.9)式对极为广泛的一类无限长序列(譬如例5.1和例5.2中的信号)也是成立的。在信号为无限长的情况下，还是必须要考虑分析公式(5.9)式中无穷项求和的收敛问题。保证这个和式收敛而对 $ x[n] $ 所加的条件是与连续时间傅里叶变换的收敛条件直接相对应的 $ ^{①} $。如果 $ x_{1}^{n} $ 是绝对可和的，即

$$
\sum_{n=-\infty}^{+\infty}|x[n]|<\infty
$$

或者，如果这个序列的能量是有限的，即

$$
\sum_{n=-\infty}^{+\infty}1\ x[n]\,|^{2}<\infty
$$

那么，(5.9)式就一定收敛。

与分析公式(5.9)式的情况相比，综合公式(5.8)式的积分是在一个有限的积分区间上进行的，因此一般不存在收敛问题。这一点与离散时间傅里叶级数综合公式(3.94)式的情况是非常相像的，在那里由于只涉及一个有限项和式，所以也就没有任何收敛问题存在。特别是，若用在频率范围为 $ |\omega| \leq W $ 内的复指数信号的积分来近似一个非周期信号 $ x[n] $ 的话，即

$$
\stackrel{\wedge}{x}[n]=\frac{1}{2\pi}\int_{-W}^{W}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega
$$

那么，若 $ W = \pi $，则有 $ x[n] = x[n] $。因此，就像图3.18那样，在求离散时间傅里叶变换综合公式时，看不到任何类似于吉伯斯现象的行为存在！这一点可用下例来说明。

**例 5.4 令 x[n] 是一单位脉冲序列**

$$
x[n]=\delta[n]
$$

这时由分析公式(5.9)式极易求得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=1
$$

这就是说，和连续时间情况一样，单位脉冲序列的傅里叶变换在所有频率上都是相等的。如果将(5.15)式用到这个例子中来，就得到

$$
\stackrel{h}{x}\left[n\right]=\frac{1}{2\pi}\int_{-W}^{W}\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega=\frac{\sin W_{n}}{\pi n}
$$

对应于几个不同的 W 值， $ \hat{x}[n] $ 图示于图 5.7 中。由图可见，当 W 增加时，近似式 $ \hat{x}[n] $ 的振荡频率就增加，这一点很像在连续时间情况下所观察到的一样；但是，另一方面，与连续时间情况相反，这些振荡的幅度相对于 $ \hat{x}[0] $ 的幅度来说，则随着 W 的增大而减小，直至 $ W = \pi $ 时，这些振荡完全消失。

![图像（物理页 285，第 1 幅）](../Figures/fig-p0285-01.jpg){#fig:p285-1}

### 5.2 周期信号的傅里叶变换 {#sec:5-2}

和在连续时间情况相同，利用把一个周期信号的变换表示成频域中的冲激串的办法，就可以把离散时间周期信号也归并到离散时间傅里叶变换的范畴中去。为了导出这种表示的形式，考虑如下信号：

$$
x[n]=\mathrm{e}^{\mathrm{j}\omega_{0}n}
$$

在连续时间情况下，已经看到 $ e^{\omega_{0}t} $ 的傅里叶变换就是在 $ \omega = \omega_{0} $ 处的冲激。因此，可以期望对离散时间情况下的(5.17)式的变换，或许会有相同的结果。然而，离散时间傅里叶变换对 $ \omega $ 来说必须是周期的，周期为 $ 2\pi $。由此可以想到，(5.17)式 x[n] 的傅里叶变换应该是在 $ \omega_{0}, \omega_{0} \pm 2\pi, \omega_{0} \pm 4\pi, \cdots $ 等处的冲激。事实上，x[n] 的傅里叶变换正是如下的冲激串

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{l=-\infty}^{+\infty}2\pi\delta(\omega-\omega_{0}-2\pi l)
$$

如图5.8所示。为了验证该式，必须求出(5.18)式的反变换。现将(5.18)式代入综合公式

![图像（物理页 286，第 1 幅）](../Figures/fig-p0286-01.jpg){#fig:p286-1}

**图 5.8 $ x[n] = e^{j\omega_0 n} $ 的傅里叶变换**

(5.8)式可得

$$
\frac{1}{2\pi}\int_{2\pi}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega=\frac{1}{2\pi}\int_{2\pi l=-\infty}^{+\infty}2\pi\delta(\omega-\omega_{0}-2\pi l)\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega
$$

注意，在任意一个长度为 $ 2\pi $ 的积分区间内，在(5.18)式的和式中真正包括的只有一个冲激，因此，如果所选的积分区间包含在 $ \omega_{0} + 2\pi r $ 处的冲激，那么

$$
\begin{array}{c}1\\ 2\pi\int_{2\pi}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega=\mathrm{e}^{\mathrm{j}(\omega_{0}+2\pi r)n}=\mathrm{e}^{\mathrm{j}\omega_{0}n}\end{array}
$$

现在考虑一周期序列 x[n]，周期为 N，其傅里叶级数为

$$
x\left[n\right]=\sum_{k\sim(N)}a_{k}e^{i k(2\pi/N)n}
$$

这时，傅里叶变换就是

$$
X(e^{j\omega})=\sum_{k=-\infty}^{+\infty}2\pi a_{k}\delta\bigg(\omega-\frac{2\pi k}{N}\bigg)
$$

这样，一个周期信号的傅里叶变换就能直接从它的傅里叶系数得到。

为了证明(5.20)式是对的，只要注意到(5.19)式的 $ x[n] $是(5.17)式这类信号的线性组合，因此 $ x[n] $的傅里叶变换也一定是(5.18)式这类变换形式的线性组合。特别是，如果选取(5.19)式的求和区间为 $ k=0,1,\cdots,N-1 $，而有

$$
x[n]=a_{0}-a_{1}\mathrm{e}^{\mathrm{j}(2\pi/N)n}+a_{2}\mathrm{e}^{\mathrm{j}2(2\pi/N)n}+\cdots+a_{N-1}\mathrm{e}^{\mathrm{j}(N-1)(2\pi/N)n}
$$

这样， $ x[n] $ 就是如 (5.17) 式所示信号的线性组合，其中 $ \omega_0 = 0, 2\pi/N, 4\pi/N, \cdots $， $ (N-1)2\pi/N $。所得到的傅里叶变换如图 5.9 所示。在图 5.9(a) 中示出 (5.21) 式右边第一项的傅里叶变换：常数序列 $ a_0 = a_0 e^{j\omega n} $ 的傅里叶变换，按 (5.18) 式，就是 $ \omega_0 = 0 $，每个冲激的大小为 $ 2\pi a_0 $ 的周期冲激串。再者，根据第 4 章的讨论知道，这些傅里叶系数 $ a_k $ 都是周期的，周期为 $ N $，所以有 $ 2\pi a_0 = 2\pi a_N = 2\pi a_{-N} $。图 5.9(b) 是 (5.21) 式中第二项的傅里叶变换，这里再次应用 (5.18) 式的结果，并且有 $ 2\pi a_1 = 2\pi a_{N+1} = 2\pi a_{-N+1} $。相类似，图 5.9(c) 是最后一项的傅里叶变换。最后，图 5.9(d) 就是整个 $ X(e^{j\omega}) $。应该注意，由于 $ a_k $ 的周期性， $ X(e^{j\omega}) $ 就能看作发生在基波频率 $ 2\pi/N $ 的整倍数频率上的一串冲激，位于 $ \omega = 2\pi k/N $ 处的冲激面积是 $ 2\pi a_k $。这就是 (5.20) 式所表达的意思。

![图像（物理页 287，第 1 幅）](../Figures/fig-p0287-01.jpg){#fig:p287-1}

![图像（物理页 287，第 2 幅）](../Figures/fig-p0287-02.jpg){#fig:p287-2}

**(b)**

![图像（物理页 287，第 3 幅）](../Figures/fig-p0287-03.jpg){#fig:p287-3}

**(c)**

![图像（物理页 287，第 4 幅）](../Figures/fig-p0287-04.jpg){#fig:p287-4}

**图 5.9 一个离散时间周期信号的傅里叶变换：**

(a) (5.21)式右边第一项的傅里叶变换；(b) (5.21)式第二项的傅里叶变换；

(c) (5.21)式最后一项的傅里叶变换；(d) (5.21)式 $ x[n] $的傅里叶变换

**例 5.5 考虑周期信号**

$$
x[n]=\cos\omega_{0}n=\frac{1}{2}\mathrm{e}^{\mathrm{j}\omega_{0}\pi}+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega_{0}\pi},\qquad\omega_{0}=\frac{2\pi}{5}
$$

根据(5.18)式，可立即写出

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{l=-\infty}^{+\infty}\pi\delta\Big(\omega-\frac{2\pi}{5}-2\pi l\Big)+\sum_{l=-\infty}^{+\infty}\pi\delta\Big(\omega+\frac{2\pi}{5}-2\pi l\Big)
$$

也就是

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\pi\delta\left(\omega-\frac{2\pi}{5}\right)+\pi\delta\left(\omega+\frac{2\pi}{5}\right),\quad-\pi\leqslant\omega<\pi
$$

$ X(e^{j\omega}) $ 以周期为 $ 2\pi $，周期重复，如图 5.10 所示。

![图像（物理页 288，第 1 幅）](../Figures/fig-p0288-01.jpg){#fig:p288-1}

**图 5.10 $ x[n]=\cos\omega_{0}n $ 的离散时间傅里叶变换**

例 5.6 与例 4.8 的周期冲激串相对应的离散时间冲激串是序列为

$$
x[n]=\sum_{k=-\infty}^{+\infty}\delta[n-k N]
$$

如图5.11(a)所示。这个信号的傅里叶级数系数能由(3,95)式直接算出来为

$$
a_{k}=\frac{1}{N}\sum_{n=(N)}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n}
$$

![图像（物理页 288，第 2 幅）](../Figures/fig-p0288-02.jpg){#fig:p288-2}

**(a)**

![图像（物理页 288，第 3 幅）](../Figures/fig-p0288-03.jpg){#fig:p288-3}

**(b)**

**图 5.11 (a) 离散时间周期冲激串; (b) (a) 的傅里叶变换**

选取求和区间为 $ 0 \leq n \leq N - 1 $，有

$$
a_{k}=\frac{1}{N}
$$

利用(5.26)和(5.20)式，该信号的傅里叶变换就能表示为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{2\pi}{N}\sum_{k=-\infty}^{+\infty}\delta\Big(\omega-\frac{2\pi k}{N}\Big)
$$

如图 5.11(b) 所示。

### 5.3 离散时间傅里叶变换性质 {#sec:5-3}

与连续时间傅里叶变换一样，离散时间傅里叶变换的各种性质也提供了对变换本质的进一步了解，同时往往在简化一个信号的正变换和反变换的求取上是很有用的。这一节及下面两节将考虑这些性质，并将这些性质简明扼要地综合于表5.1中。将表5.1和表4.1作一比较就会发现，连续时间和离散时傅里叶变换性质之间所呈现出的相似和差别。当某一性质在推导及陈述上基本上与连续时间情况下是一样的话，那么就从简。同时，由于傅里叶级数和傅里叶变换之间的紧密关系，因此就将傅里叶变换的很多性质直接移至离散时间傅里叶级数的相应性质中去。这些性质已经列于表3.2中，并在3.7节作过简要讨论。

在以下的讨论中，与4.3节一样，采用如下符号来表明一个信号及其傅里叶变换的一对关系，即

$$
X(e^{j\omega})=\mathcal{F}|_{x}[n]\}
$$

$$
x[n]=\mathcal{F}^{1}\{X(\mathrm{e}^{\mathrm{j}\omega})\}
$$

$$
x[n]\overset{\mathcal{F}}{\leftrightarrow}X(\mathrm{e}^{\mathrm{j}\omega})
$$

#### 5.3.1 离散时间傅里叶变换的周期性 {#sec:5-3-1}

如同在5.1节所讨论的，离散时间傅里叶变换对ω来说总是周期的，其周期为 $ 2\pi $，即

$$
X(\mathrm{e}^{\mathrm{j}(\omega+2\pi)})=X(\mathrm{e}^{\mathrm{j}\omega})
$$

这点与连续时间傅里叶变换是不同的，一般来说，后者不是周期的。

#### 5.3.2 线性 {#sec:5-3-2}

若

$$
x_{1}[n]{\overset{\mathcal{T}}{\leftrightarrow}}X_{1}(\mathrm{e}^{\mathrm{j}\omega})
$$

和

$$
x_{2}[n]{\overset{\mathcal{S}}{\leftrightarrow}}X_{2}(\mathrm{e}^{\mathrm{j}\omega})
$$

则

$$
a x_{1}[n]+b x_{2}[n]\stackrel{\mathcal{F}}{\leftrightarrow}a X_{1}(\mathrm{e}^{\mathrm{j}\omega})+b X_{2}(\mathrm{e}^{\mathrm{j}\omega})
$$

#### 5.3.3 时移与频移性质 {#sec:5-3-3}

若

$$
x[n]{\overset{\mathcal{F}}{\leftrightarrow}}X(e^{j\omega})
$$

则有

$$
x[n-n_{0}]\stackrel{\mathcal{F}}{\leftrightarrow}\mathrm{e}^{-\mathrm{j}\omega n_{0}}X(\mathrm{e}^{\mathrm{j}\omega})
$$

和

$$
\mathrm{e}^{\mathrm{j}\omega_{0}n}x[n]\leftrightarrow X(\mathrm{e}^{\mathrm{j}(\omega-\omega_{0})})
$$

将 $ x[n-n_{0}] $ 直接代入分析公式(5.9)式就可得到(5.30)式，而将 $ X(\mathrm{e}^{\mathrm{j}(\omega-\omega_{0})}) $ 代入综合公式(5.8)式就可导出(5.31)式。

作为离散时间傅里叶变换周期性和频移性质的一个结果，就是在理想低通和理想高通离散时间滤波器之间存在的一种特别关系。

例 5.7 图 5.12(a) 示出一个截止频率为 $ \omega_{k} $ 的低通滤波器的频率响应 $ H_{lp}(e^{j\omega}) $，而图 5.12(b) 则是将 $ H_{lp}(e^{j\omega}) $ 频移半个周期（即 $ \pi $）后的 $ H_{lp}(e^{j(\omega-\pi)}) $。因为在离散时间情况下，高频是集中在 $ \pi $（或 $ \pi $ 的奇数倍）附近，所以图 5.12(b) 所示特性就是一个截止频率为 $ \pi - \omega_{k} $ 的理想高通滤波器，也即

$$
H_{\mathrm{h p}}(\mathrm{e}^{\mathrm{j}\omega})=H_{\mathrm{l p}}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})
$$

**(a)**

![图像（物理页 290，第 1 幅）](../Figures/fig-p0290-01.jpg){#fig:p290-1}

![图像（物理页 290，第 2 幅）](../Figures/fig-p0290-02.jpg){#fig:p290-2}

由(3.122)式可知，并且在5.4节将再次讨论的，一个LTI系统的频率响应是该系统单位脉冲响应的傅里叶变换，于是，若 $ h_{lp}[n] $和 $ h_{lp}[n] $分别记作图5.12(a)

**(b)**

**图 5.12 (a) 某一低通滤波器的频率响应；**

**(b) 将(a)的频率响应频移半个周期 $ \omega = \pi $ 得到一高通滤波器的频率响应**

和(b)的单位脉冲响应，那么(5.32)式和频移性质就意味着低通和高通滤波器有如下关系：

$$
h_{\mathrm{f p}}\left[n\right]=\mathrm{e}^{\mathrm{j}\pi n}h_{\mathrm{f p}}\left[n\right]
$$

$$
=(-1)^{n}h_{\mathrm{p}}\left[n\right]
$$

#### 5.3.4 共轭与共轭对称性 {#sec:5-3-4}

若

$$
x[n]\overset{\tau_{*}}{\leftrightarrow}X(\mathrm{e}^{\mathrm{j}\omega})
$$

则

$$
\left[\begin{array}{c}x^{*}\left[n\right]^{\mathcal{F}}\leftrightarrow X^{*}\left(\mathrm{e}^{-\mathrm{j}\omega}\right)\end{array}\right]
$$

同时，若 x[n] 是实值序列，那么其变换是共轭对称的，即

$$
X(\mathrm{e}^{\mathrm{j}\omega})=X^{*}(\mathrm{e}^{-\mathrm{j}\omega})\quad[x[n] 为实]
$$

据此可得， $ \mathcal{P}_{e}\{X(e^{j\omega})\} $ 是 $ \omega $ 的偶函数，而 $ \mathcal{I}_{m}\{X(e^{j\omega})\} $ 是 $ \omega $ 的奇函数。同理， $ X(e^{j\omega}) $ 的模是 $ \omega $ 的偶函数，相角是 $ \omega $ 的奇函数。另外进一步可得

$$
\mathcal{E}_{u}\{X[~n~]\}\overset{\mathcal{F}}{\leftrightarrow}\mathcal{R}_{e}\{X(\mathrm{e}^{\mathrm{j}\omega})\}
$$

和

$$
\mathcal{O}_{d}\{x[n]\}\overset{\mathcal{T}}{\longleftrightarrow}j\mathcal{I}_{m}\{X(\mathrm{e}^{\mathrm{j}\omega})\}
$$

这里， $ E_{u} $ 和 $ Q_{d} $ 分别表示 x[n] 的偶部和奇部。例如，若 x[n] 为实且为偶序列，那么其傅里叶变换也是实且为偶函数。例 5.2 对序列 x[n] = a^{|n|} 就说明了这种对称性。

离散时间情况下的累加就相应于连续时间情况下的积分。现在来讨论离散时间序列的累加及其逆运算——一次差分的傅里叶变换。设 $ x[n] $ 的傅里叶变换为 $ X(e^{j\omega}) $，那么根据线性和时移性质。一次差分信号 $ x[n]-x[n-1] $ 的傅里叶变换对就是

#### 5.3.5 差分与累加 {#sec:5-3-5}

$$
x[n]-x[n-1]{\overset{\mathcal{F}}{\leftrightarrow}}(1-\mathrm{e}^{-\mathrm{i}\omega})X(\mathrm{e}^{\mathrm{i}\omega})
$$

再考虑信号

$$
y[n]=\sum_{m=-\infty}^{\pi}x[m]
$$

因为 $ y[n] - y[n-1] = x[n] $，似乎可能得出 $ y[n] $ 的变换应为 $ x[n] $ 的变换被 $ (1 - e^{-1\omega}) $ 所除！但是，这只是对了一部分，像(4.32)式所给出的连续时间积分性质一样，除此以外，还会涉及到更多的项。其精确的关系是

$$
\sum_{m=-\infty}^{n}x[m]\leftrightarrow\frac{1}{1-\mathrm{e}^{-\mathrm{j}\omega}}X(\mathrm{e}^{\mathrm{j}\omega})+\pi X(\mathrm{e}^{\mathrm{j}0})\sum_{k=-\infty}^{+\infty}\delta(\omega-2\pi k)
$$

式中右边的冲激串反映了累加过程中可能出现的直流或平均值。

例 5.8 现利用累加性质来导出单位阶跃 x[n]=u[n] 的傅里叶变换 $ X(e^{j\omega}) $。已知

$$
g[n]=\delta[n]{\stackrel{\beta}{\leftrightarrow}}G(\mathrm{e}^{\mathrm{j}\omega})=1
$$

自1.4.1节知道，单位阶跃就是单位脉冲的累加，即

$$
x[n]=\sum_{m=-\infty}^{n}g[m]
$$

上式两边取傅里叶变换，并应用累加性质可得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{(1-\mathrm{e}^{-\mathrm{j}\omega})}G(\mathrm{e}^{\mathrm{j}\omega})+\pi G(\mathrm{e}^{\mathrm{j}0})\sum_{k=-\infty}^{\infty}\delta(\omega-2\pi k)\\ =\frac{1}{1-\mathrm{e}^{-\mathrm{j}\omega}}+\pi\sum_{k=-\infty}^{\infty}\delta(\omega-2\pi k)
$$

#### 5.3.6 时间反转 {#sec:5-3-6}

设信号 $ x[n] $ 的频谱为 $ X(e^{j\omega}) $，考虑一下 $ y[n]=x[-n] $ 的变换 $ Y(e^{j\omega}) $。由(5.9)式

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}y[n]\mathrm{e}^{-\mathrm{j}\omega n}=\sum_{n=-\infty}^{+\infty}x[-\ n]\mathrm{e}^{-\mathrm{j}\omega n}
$$

在(5.40)式中作 m = -n 置换，得

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\sum_{m=-\infty}^{+\infty}x[m]\mathrm{e}^{-\mathrm{j}(-\omega)m}=X(\mathrm{e}^{-\mathrm{j}\omega})
$$

也即

$$
x[-n]^{\frac{g}{2}}\leftrightarrow X(e^{-j\omega})
$$

#### 5.3.7 时域扩展 {#sec:5-3-7}

由于离散时间信号在时间上的离散性，因此时间和频率的尺度变换性质与在连续时间下相比都稍许有些不同。在4.3.5节曾导出连续时间下的性质为

$$
x(a t)\stackrel{\mathcal{T}}{\leftrightarrow}\frac{1}{\mid a\mid}X\left(\frac{\mathrm{j}\omega}{a}\right)
$$

然而，如果试图要定义一个信号 $x[an]$，若 $a$ 不是一个整数时就遇到了困难。因此就不能用 $a<1$ 来减慢这个信号的变化；另一方面，就是令 $a$ 是一个不同于 $\pm1$ 的整数，比如说考虑 $x[2n]$，这也不只是使原信号的变化加速。因为 $n$ 仅仅取整数值，$x[2n]$ 仅为由 $x[n]$ 中的偶次样本所组成。

然而，若令 k 是一个正整数，并且定义

$$
x_{(k)}\left[n\right]=\left\{\begin{aligned}&x\left[n/k\right]\quad& 当 n 为 k 的整倍数 \\ &0,\quad& 当 n 不为 k 的整倍数 \end{aligned}\right.
$$

那么，则有一个与(5.43)式相并行的结果。图5.13示出一个k=3的例子，这时的 $ x_{(k)}[n] $是在 $ x[n] $的连续值之间插入(k-1)个零值而得到的。直观上来看，可以把 $ x_{(k)}[n] $看作是减慢了的 $ x[n] $。因为，除非n是k的某一倍数，也即n=rk，否则 $ x_{(k)}[n] $都等于0，所以 $ x_{(k)}[n] $的傅里叶变换可由下式给出

$$
X_{(k)}\bigl(\mathrm{e}^{\mathrm{j}\omega}\bigr)\;=\;\sum_{n=-\infty}^{+\infty}x_{(k)}\bigl[n\bigr]\mathrm{e}^{-\mathrm{j}\omega n}\;=\;\sum_{r=-\infty}^{+\infty}x_{(k)}\bigl[r k\bigr]\mathrm{e}^{-\mathrm{j}\omega r k}
$$

![图像（物理页 292，第 1 幅）](../Figures/fig-p0292-01.jpg){#fig:p292-1}

![图像（物理页 292，第 2 幅）](../Figures/fig-p0292-02.jpg){#fig:p292-2}

**图 5.13 在序列 x[n] 的每两个连续值之间插入两个零值而得到的序列 $ x_{(3)}[n] $**

再者，由于 $ x_{(k)}[rk]=x[r] $，可求得

$$
X_{(k)}(\mathrm{e}^{\mathrm{j}\omega})=\sum_{r=-\infty}^{+\infty}x[r]\mathrm{e}^{-\mathrm{j}(k\omega)r}=X(\mathrm{e}^{\mathrm{j}k\omega})
$$

也即

$$
\boxed{x_{(k)}[n]^{\frac{q}{k}}\xrightarrow{f}X(e^{jk\omega})}
$$

应该注意到，当取 k>1 时，该信号在时间上被拉开了，从而在时间上就减慢了，而它的

傅里叶变换就受到压缩。例如，由于 $ X(e^{j\omega}) $ 是周期的，周期为 $ 2\pi $，因而 $ X(e^{j\omega}) $ 也是周期的，其周期为 $ 2\pi/k $。图 5.14 示出一个矩形脉冲的例子来说明这一性质。

![图像（物理页 293，第 1 幅）](../Figures/fig-p0293-01.jpg){#fig:p293-1}

![图像（物理页 293，第 2 幅）](../Figures/fig-p0293-02.jpg){#fig:p293-2}

![图像（物理页 293，第 3 幅）](../Figures/fig-p0293-03.jpg){#fig:p293-3}

![图像（物理页 293，第 4 幅）](../Figures/fig-p0293-04.jpg){#fig:p293-4}

**图 5.14 时域和频域之间的相反关系：当 k 增加时， $ x_{(k)}[n] $ 在时域上拉开，而其变换则在频域上压缩**

例 5.9 作为时域扩展性质在确定傅里叶变换应用中的一个例子，让我们来考虑一下示于图 5.15(a) 中的序列。可以将这个序列与图 5.15(b) 这一较为简单的序列联系起来，这就是

$$
x[n]=y_{(2)}[n]+2y_{(2)}[n-1]
$$

其中

$$
y_{(2)}[n]=\left\{\begin{aligned}&y[n/2],&\quad 当 \ n\  为偶 \\ &0,&\quad 当 \ n\  为奇 \end{aligned}\right.
$$

而 $ y_{(2)}[n-1] $ 则代表 $ y_{(2)}[n] $ 右移一个单位。信号 $ y_{2}[n] $ 和 $ 2y_{(2)}[n-1] $ 均分别示于图 5.15(c) 和 (d)。

接下来可以看到， $ y[n]=g[n-2]^{\textcircled{1}} $， $ g[n] $就是曾在例5.3中讨论过的当 $ N_{1}=2 $时的矩形脉冲，并示于图5.6(a)中。结果，根据例5.3和时移性质，有

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\mathrm{e}^{-\mathrm{j}2\omega}\frac{\sin(5\omega/2)}{\sin(\omega/2)}
$$

利用时域扩展性质可得

$$
y_{(2)}[n]\stackrel{ 记 }{\rightarrow}\mathrm{e}^{-j4\omega}\frac{\sin(5\omega)}{\sin(\omega)}
$$

再根据线性和时移性质有

$$
2y_{(2)}\big[n-1\big]\overset{\beta}{\leftrightarrow}2\mathrm{e}^{-\mathrm{j}\beta\omega}\frac{\sin(5\omega)}{\sin(\omega)}
$$

将以上两个结果合在一起，最后得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\mathrm{e}^{-\mathrm{j}4\omega}(1+2\mathrm{e}^{-\mathrm{j}\omega})\left(\frac{\sin(5\omega)}{\sin(\omega)}\right)
$$

**(a)**

设

![图像（物理页 294，第 1 幅）](../Figures/fig-p0294-01.jpg){#fig:p294-1}

![图像（物理页 294，第 2 幅）](../Figures/fig-p0294-02.jpg){#fig:p294-2}

#### 5.3.8 频域微分 {#sec:5-3-8}

**(b)**

$$
x[n]{\overset{,}{\leftrightarrow}}X(\mathrm{e}^{\mathrm{j}\omega})
$$

这个性质的用途将在5.4节例5.13中说明。

$$
nx[n]^{\frac{j}{2}}\mathrm{j}\frac{\mathrm{d}X(\mathrm{e}^{\mathrm{j}w})}{\mathrm{d}\omega}
$$

如果利用分析公式(5.9)式 $ X(e^{j\omega}) $ 的定义，并在两边对 $ \omega $ 微分，可得

这个式子的右边就是 $ -\ln x $ [n] 的傅里叶变换，因此两边各乘以 j，就得

$$
\frac{\mathrm{d}X(\mathrm{e}^{\mathrm{j}\omega})}{\mathrm{d}\omega}=\sum_{n=-\infty}^{+\infty}-\mathrm{j}nx[n]\mathrm{e}^{-\mathrm{j}\omega n}
$$

![图像（物理页 294，第 3 幅）](../Figures/fig-p0294-03.jpg){#fig:p294-3}

![图像（物理页 294，第 4 幅）](../Figures/fig-p0294-04.jpg){#fig:p294-4}

**(d)**

**图 5.15 (a) 例 5.9 的信号 x[n]; (b) 信号 y[n];**

**(c) 由 y[n] 每两点之间插入一个零值所得到的信号 $ y_{(2)}[n] $;**

（d）信号 $ 2y_{(2)}[n-1] $

#### 5.3.9 帕斯瓦尔定理 {#sec:5-3-9}

若 x[n] 和 $ X(e^{j\omega}) $ 是一对傅里叶变换，则

$$
\sum_{n=-\infty}^{+\infty}\mid x[n]\mid^{2}=\frac{1}{2\pi}\int_{2\pi}\mid X(\mathrm{e}^{\mathrm{j}\omega})\mid^{2}\mathrm{d}\omega
$$

这个关系很类似于(4.43)式，并且推导过程也很类似。该(5.47)式左边的量就是在信号 $ x[n] $中的总能量，帕斯瓦尔定理表明这个总能量可以在离散时间频率的 $ 2\pi $区间上用积分每单位频率上的能量 $ |X(e^{j\omega})|^2/2\pi $来获得。与连续时间情况相仿， $ |X(e^{j\omega})|^2 $称为信号 $ x[n] $的能量密度谱。同时也注意到，(5.47)式是与周期信号的帕斯瓦尔定理(3.110)式相对应的，在那里说的是：在一个周期信号中的平均功率等于它的各次谐波分量的平均功率之和。

已知一个序列的傅里叶变换，就有可能根据傅里叶变换的性质来确定是否某一特殊的序列有某些不同的性质。现在用下面的例子来说明这一概念。

例 5.10 考虑序列 x[n]，其傅里叶变换 $ X(e^{j\omega}) = -\pi \leq \omega \leq \pi $ 区间上示于图 5.16。现在要想确定在时域 x[n] 是否是周期的，实信号，偶信号和/或有限能量的。

首先注意到，在时域上的周期性就意味着其傅里叶变换除了在各个基波频率的整倍数频率上有可能出现冲激外，其余地方均为零。现在 $ X(e^{ju}) $ 不是这样，所以得出： $ x[n] $ 不是周期的。

接下来，根据傅里叶变换的对称性知道，一个实值序列一定有一个傅里叶变换，其模是 $ \omega $的偶函

数，相位是 $ \omega $ 的奇函数。对于给出的 $ \left|X\left(\mathrm{e}^{\mathrm{i}\omega}\right)\right| $ 和 $ \left\{X\left(\mathrm{e}^{\mathrm{i}\omega}\right)\right\} $ 来看是这样，因此 $ x[n] $ 是实序列。

第三，若 $ x[n] $ 是偶函数，那么根据实信号的对称性， $ X(e^{j\omega}) $ 必须为实且偶。然而，因为 $ X(j\omega)=|X(e^{j\omega})|e^{-j2\omega},X(e^{j\omega}) $ 不是一个实值函数，因此 $ x[n] $ 不是偶信号。

最后，为了检查是否为有限能量，可以用帕斯瓦尔定程

$$
\sum_{n=-\infty}^{\infty}\mid x[n]\mid^{2}=\frac{1}{2\pi}\int_{2\pi}\mid X(e^{j\omega})\mid^{2}d\omega
$$

由图 5.16 很显然，在 $ -\pi $ 到 $ \pi $ 上积分 $ \left|X\left(\mathrm{e}^{\mathrm{j}\omega}\right)\right|^{2} $ 一定为一个有限量，所以 $ x[n] $ 是有限能量的。

在下面的各节中将讨论另外的几个性质。其中头两个就是卷积和相乘性质，这个很类似于在4.4节和4.5节所讨论过的那些性质。第三个是对偶性质，将在5.7节讨论。这里所考虑的对偶性不仅仅是离散时间域中的对偶性，而且也考虑到存在于连续时间和离散时间域之间的对偶性。

![图像（物理页 295，第 1 幅）](../Figures/fig-p0295-01.jpg){#fig:p295-1}

**图 5.16 例 5.10 中傅里叶变换的模和相位**

### 5.4 卷积性质 {#sec:5-4}

在4.4节曾经就连续时间傅里叶变换在处理卷积运算，以及涉及在连续时间LTI系统应用中的重要性作过讨论。在离散时间情况下也有完全相同的关系，并且这也就是离散时间傅里叶变换在表示和分析离散时间LTI系统中具有如此重要价值的主要原因之一。若 $ x[n] $， $ h[n] $和 $ y[n] $分别为某一LTI系统的输入、单位脉冲响应和输出，而有

$$
y[n]=x[n]*h[n]
$$

那么

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=X(\mathrm{e}^{\mathrm{j}\omega})H(\mathrm{e}^{\mathrm{j}\omega})
$$

式中 $ X(\mathrm{e}^{\mathrm{j}\omega}) $, $ H(\mathrm{e}^{\mathrm{j}\omega}) $ 和 $ Y(\mathrm{e}^{\mathrm{j}\omega}) $ 分别为 $ x[n] $, $ h[n] $ 和 $ y[n] $ 的傅里叶变换。将 (3.122) 式与 (5.9) 式作一比较就可看出，一个离散时间 LTI 系统的频率响应，如同第一次在 3.8 节所定义的，就是该系统单位脉冲响应的傅里叶变换。

(5.48)式的导出可完全与4.4节的导出过程一样来进行。尤其是，与连续时间情况相同，对 $ x[n] $的综合公式(5.8)式可以看作是将 $ x[n] $分解成一组复指数信号的线性组合，其中每个复指数信号的振幅都是无限小，而且正比于 $ X(e^{j\omega}) $，并且每一个复指数信号都是系统的特征函数。在第3章正是应用这一点证明了，一个LTI系统对一个周期信号响应的傅里叶级数系数就是输入的傅里叶系数乘以该系统频率响应在相应谐波频率上的值。卷积性质(5.48)式代表了这一结果对于非周期输入和输出情况下的推广，不过所用的是傅里叶变换，而不是傅

里叶级数。

与连续时间情况一样，(5.48)式将两个信号的卷积转化为它们的傅里叶变换相乘这样简单的代数运算，这一点既方便于信号与系统的分析，又大大深化了一个LTI系统对施加于它的输入信号的响应这一问题的理解。特别是，从(5.48)式可见，频率响应 $ H(e^{j\omega}) $控制了输入的傅里叶变换在每一频率 $ \omega $上复振幅的变化，因此，在频率选择性滤波中，就要求在相应于所需要的通带频率范围内 $ H(e^{j\omega})\approx1 $，而在需要消除或大大衰减的频带内 $ H(e^{j\omega})\approx0 $。

#### 5.4.1 举例 {#sec:5-4-1}

为了说明卷积性质以及其它几个性质的应用，本节研究以下几个例子。

**例 5.11 考虑一 LTI 系统，其单位脉冲响应为**

$$
h[n]=\delta[n-n_{0}]
$$

它的频率响应 $ H(e^{j\omega}) $就是

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}\delta[n-n_{0}]\mathrm{e}^{-\mathrm{j}\omega n}=\mathrm{e}^{-\mathrm{j}\omega n_{0}}
$$

因此，对于傅里叶变换为 $ X(e^{j\omega}) $ 的任意输入 $ x[n] $，其输出的傅里叶变换是

$$
Y(e^{\mathrm{j}\omega})=\mathrm{e}^{-\mathrm{j}\omega n_{0}}X(e^{\mathrm{j}\omega})
$$

对于这个例子， $ y[n] = x[n - n_0] $，(5.49)式就与时移性质相一致。同时，频率响应 $ H(e^{j\omega}) = e^{-j\omega n_0} $，它是一个纯时移系统，对所有频率其模为1，而相移则与频率成线性关系，即 $ -\omega n_0 c $

例 5.12 考虑一下在 3.9.2 节介绍过的离散时间理想低通滤波器。该系统的频率响应 $ H(e^{j\omega}) $ 如图 5.17(a) 所示。因为一个 LTI 系统的单位脉冲响应和频率响应是一对傅里叶变换，所以就能利用傅里叶变换的综合公式 (5.8) 式由频率响应来确定该理想低通滤波器的单位脉冲响应。以 $ -\pi \leq \omega \leq \pi $ 作为积分区间，由图 5.17(a) 可见有

$$
h\left[n\right]=\frac{1}{2\pi}\int_{-\pi}^{\pi}H(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega=\frac{1}{2\pi}\int_{-\omega_{c}}^{\omega_{c}}\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega=\frac{\sin\omega_{c}n}{\pi n}
$$

h[n]如图5.17(b)所示。

![图像（物理页 296，第 1 幅）](../Figures/fig-p0296-01.jpg){#fig:p296-1}

![图像（物理页 296，第 2 幅）](../Figures/fig-p0296-02.jpg){#fig:p296-2}

**图 5.17 (a) 离散时间理想低通滤波器的频率响应；**

（b）该理想低通滤波器的单位脉冲响应

在图5.17中，遇到了许多同样的问题，这些问题曾在例4.18的连续时间理想低滤波器中出现过。首先，因为 $ h[n] $在n<0不为零，因此该理想低通滤波器不是因果的。第二，即便因果性不是一个重要的因素，也还是有一些其它的原因而选择用非理想滤波器来实现频率选择性滤波，这里面包括易于实现以及对时域特性的一些要求等等。特别是，图5.17(b)的理想低通滤波器的单位脉冲响应是振荡型的，这一点在其应用中是不希望有用。在这样一些情况下，必须在频域要求（如频率选择性）和时域特性（如非振荡性）之间作出某一折衷。第6章将详细讨论这些问题及其有关的概念。

下面的例子用来说明，卷积性质在卷积和的计算上也是很有用的。

**例 5.13 考虑一 LTI 系统，其单位脉冲响应为**

$$
h[n]=\alpha^{n}u[n]
$$

这里 $ |\alpha|<1 $。假设该系统的输入是

$$
x[n]=\beta^{n}u[n]
$$

$ |\beta|<1 $。求 $ h[n] $和 $ x[n] $的傅里叶变换，有

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}
$$

和

$$
X(e^{j\omega})=\frac{1}{1-\beta e^{-j\omega}}
$$

这样就有

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=H(\mathrm{e}^{\mathrm{j}\omega})X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{(1-\alpha\mathrm{e}^{-\mathrm{j}\omega})(1-\beta\mathrm{e}^{-\mathrm{j}\omega})}
$$

和例4.19相同，求 $ Y(e^{j\omega}) $的反变换，最容易的做法就是用部分分式将 $ Y(e^{j\omega}) $展开。 $ Y(e^{j\omega}) $是以 $ e^{-j\omega} $的两个多项式之比，总是愿意将它表示成比较简单的一些项之和，这样用直观(或许再结合利用5.3.8节的频率微分性质)就能求得每一项的反变换。对于有理变换的一般代表运算步骤在附录中给予讨论。对于本例，若 $ \alpha\neq\beta $。 $ Y(e^{j\omega}) $的部分分式展开就具有如下形式：

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\frac{A}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}+\frac{B}{1-\beta\mathrm{e}^{-\mathrm{j}\omega}}
$$

将(5.53)式和(5.54)式的右边令其相等，就得

$$
A=\frac{\alpha}{\alpha-\beta},B=-\frac{\beta}{\alpha-\beta}
$$

因此，根据例5.1和线性性质，凭直观就得(5.54)式的反变换为

$$
y[n]=\frac{\alpha}{\alpha-\beta}\alpha^{n}u[n]-\frac{\beta}{\alpha-\beta}\beta^{}u[n]=\frac{1}{\alpha-\beta}[\alpha^{n+1}u[n]-\beta^{n+1}u[n]]
$$

若 $ \alpha = \beta, (5.54) $ 式的部分分式展开式就不成立，然而，这时

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\left(\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}\right)^{2}
$$

这就能表示成

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\frac{\mathrm{j}}{\alpha}\mathrm{e}^{\mathrm{j}\omega}\frac{\mathrm{d}}{\mathrm{d}\omega}\left(\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}\right)
$$

和例4.19相同，可以利用频域微分性质(5.46)式，再结合傅里叶变换对

$$
\alpha^{n}u\left[n\right]\overset{\mathcal{F}}{\leftrightarrow}\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{i}\omega}}
$$

得出

$$
n\alpha^{n}u\left[n\right]\stackrel{\mathcal{F}}{\leftrightarrow}\mathrm{j}\;\frac{\mathrm{d}}{\mathrm{d}\omega}\left(\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{j}\omega}}\right)
$$

为了计及因子 $ e^{jw} $，可应用时移性质得到

$$
(n+1)\alpha^{n+i}u\lfloor n+1\rfloor\xrightarrow{\mathcal{F}}\mathrm{j e}^{\mathrm{i}\omega}\frac{\mathrm{d}}{\mathrm{d}\omega}\left(\frac{1}{1-\alpha\mathrm{e}^{-\mathrm{i}j\omega}}\right)
$$

最后再考虑到(5.56)式中的 $ 1/\alpha $因子，可得

$$
y[n]=(\boldsymbol{n}+1)\alpha^{n}u[n+1]
$$

值得注意的是，虽然上式的右边乘了一个起始于 n = -1 的阶跃，但是序列 $ (n + 1)\alpha^n u[n + 1] $ 在 n = 0 以前仍然为零，因为因子 $ (n + 1) $ 在 n = -1 时为零。因此，也能换成另一种形式将 $ y[n] $ 表示为

下面例子用以说明，卷积性质与其它傅里叶变换性质一起，在分析系统互联中往往也是很有用的。

例 5.14 考虑图 5.18(a) 的系统，其输入为 $ x[n] $，输出为 $ y[n] $。频率响应为 $ H_{lp}(e^{j\omega}) $ 的 LTI 系统是一个截止频率为 $ \pi/4 $ 的理想低通滤波器，通带内增益为 1。先考虑图 5.18(a) 中的上部路径。信号 $ w_1[n] $ 的傅里叶变换可以将 $ (-1)^n = e^{j\omega n} $ 而使得有 $ w_1[n] = e^{j\pi n}x[n] $，再利用频移性质而得到

$$
W_{1}(e^{j\omega})=X(e^{j(\omega-\pi)})
$$

**(a)**

![图像（物理页 298，第 1 幅）](../Figures/fig-p0298-01.jpg){#fig:p298-1}

由卷积性质得出

$$
W_{2}(\mathrm{e}^{\mathrm{j}\omega})=H_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}\omega})X(\mathrm{e}^{\mathrm{j}(\omega-\pi)})\nonumber
$$

因为 $ w_{3}[n] = e^{jnn} w_{2}[n] $，再

**(b)**

**图 5.18 (a) 例 5.14 中的系统互联；(b) 该系统的总频率响应**

$$
\begin{aligned}{W_{3}(\mathrm{e}^{\mathrm{j}\omega})}&{{}=W_{2}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})^{\mathrm{~\scriptsize~ 回~3~}.}}\\ {}&{{}=H_{\mathrm{l p}}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})X(\mathrm{e}^{\mathrm{j}\omega-2\pi})}\\ \end{aligned}
$$

因为离散时间傅里叶变换总是周期的，周期为 $ 2\pi $

$$
W_{3}(\mathrm{e}^{\mathrm{j}\omega})=H_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})X(\mathrm{e}^{\mathrm{j}\omega})
$$

再在图5.18(a)的下部路径应用卷积性质，可得

$$
W_{4}(\mathrm{e}^{\mathrm{j}\omega})=H_{\mathrm{p}}(\mathrm{e}^{\mathrm{j}\omega})X(\mathrm{e}^{\mathrm{j}\omega})
$$

根据傅里叶变换的线性性质，有

$$
\mathrm{Y}(\mathrm{e}^{\mathrm{j}\omega})=\mathrm{W}_{3}(\mathrm{e}^{\mathrm{j}\omega})+\mathrm{W}_{4}(\mathrm{e}^{\mathrm{j}\omega})=[\mathrm{H}_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})+\mathrm{H}_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}\omega})]\mathrm{X}(\mathrm{e}^{\mathrm{j}\omega})
$$

结果，图5.18(a)整个系统的频率响应为

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\left[H_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}(\omega-\pi)})+H_{\mathrm{lp}}(\mathrm{e}^{\mathrm{j}\omega})\right]
$$

如图5.18(b)所示。

如同在例 5.7 中所看到的， $ H_{lp}(e^{j(\omega-\pi)}) $ 是一个理想高通滤波器的频率响应。因此，整个系统既

通过低频，又通过高频，而阻止这两个频带之间的频率通过。也就是说，这是一个称之为具有理想带阻特性的滤波器，其阻带范围是 $ \pi/4 < |\omega| < 3\pi/4 $。

值得提及的是，和连续时间情况相同，不是每一个LTI系统都有一个频率响应。例如，单位脉冲响应 $ h[n]=2^{n}u[n] $的LTI系统，对正弦输入就不是一个有限的响应，这就反映出对 $ h[n] $的傅里叶变换的分析公式是发散的。然而，若一个LTI系统是稳定的，那么由2.3.7节，它的单位脉冲响应就是绝对可和的，即

$$
\sum_{n=-\infty}^{+\infty}\mid h[n]\mid<\infty
$$

因此，对稳定系统而言，频率响应总是收敛的。在利用傅里叶方法时，总是局限到单位脉冲响应的傅里叶变换存在的系统内。第10章将把傅里叶变换推广到z变换中去，在那里就可以对频率响应不收敛的LTI系统应用变换法。

### 5.5 相乘性质 {#sec:5-5}

在4.5节介绍了连续时间信号的相乘性质，并通过几个例子指出了它的某些应用。对于离散时间信号也有一个类似的性质，在应用中也起着同样的作用。这一节直接来导出这一结果，并给出一个例子来说明它的应用。到第7和第8章，将用相乘性质在采样和通信的范畴内进行讨论。

考虑 y[n] 等于 $ x_{1}[n] $ 和 $ x_{2}[n] $ 的乘积，它们的傅里叶变换分别是 $ Y(e^{j\omega}), X_{1}(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $，那么

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}y[n]\mathrm{e}^{-\mathrm{j}\omega n}=\sum_{n=-\infty}^{+\infty}x_{1}[n]x_{2}[n]\mathrm{e}^{-\mathrm{j}\omega n}
$$

或者，因为

$$
x_{1}[n]=\frac{1}{2\pi}\int_{2\pi}X_{1}(\mathrm{e}^{\mathrm{j}\theta})\mathrm{e}^{\mathrm{j}\theta n}\mathrm{d}\theta
$$

于是有

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}x_{2}[n]\left\{\frac{1}{2\pi}\int_{2\pi}X_{1}(\mathrm{e}^{\mathrm{j}\theta})\mathrm{e}^{\mathrm{j}\theta n}\mathrm{d}\theta\right\}\mathrm{e}^{-\mathrm{j}\omega n}
$$

交换求和与积分次序，可得

$$
Y(\mathrm{e}^{\mathrm{j}w})=\frac{1}{2\pi}\int_{2\pi}X_{1}(\mathrm{e}^{\mathrm{j}\theta})\Big[\sum_{n=-\infty}^{+\infty}x_{2}[n]\mathrm{e}^{-\mathrm{j}(\omega-\theta)n}\Big]\mathrm{d}\theta
$$

上式方括号内的和就是 $ X_{2}(\mathrm{e}^{\mathrm{j}(\omega-\theta)}) $，结果(5.62)式就变成

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{2\pi}\int_{2\pi}X_{1}(\mathrm{e}^{\mathrm{j}\theta})X_{2}(\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta
$$

(5.63)式就相应于 $ X_{1}(e^{j\omega}) $和 $ X_{2}(e^{j\omega}) $的周期卷积，并且在这个式子中的积分可以在任意 $ 2\pi $长度的区间内进行。卷积的一般形式(积分区间从 $ -\infty $到 $ +\infty $)常称为非周期卷积，以与周期卷积相区分。周期卷积的机理最好通过例子来说明。

例 5.15 有一信号 $ x[n] $，它为两个另外的信号的乘积，求其傅里叶变换 $ X(e^{j\omega}) $，即

$$
x[n]=x_{1}[n]x_{2}[n]
$$

式中

$$
x_{1}[n]=\frac{\sin(3\pi n/4)}{\pi n}
$$

和

$$
x_{2}[n]=\frac{\sin(\pi n/2)}{\pi n}
$$

根据(5.63)式的相乘性质知道， $ X(e^{j\omega}) $ 是 $ X_{1}(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $ 的周期卷积，其中(5.63)式的积分可以在任意 $ 2\pi $ 长度的区间内进行。现选取积分区间为 $ -\pi < \theta \leq \pi $ ①，可得

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{2\pi}\int_{-\pi}^{\pi}X_{1}(\mathrm{e}^{\mathrm{j}\theta})X_{2}(\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta
$$

(5.64)式类似于非周期卷积，除了积分是限制在区间 $ -\pi < \theta \leq \pi $ 这一点外。然而，我们可以将这个式子转换成一般的卷积，定义

$$
\hat{X}_{1}(\mathrm{e}^{\mathrm{j}\omega})=\left|\begin{aligned}X_{1}(\mathrm{e}^{\mathrm{j}\omega}),&\quad 对 -\pi<\omega\leqslant\pi\\0,&\quad 其余 \omega\end{aligned}\right.
$$

然后，在(5.64)式中用 $ \hat{X}_{1}(e^{j\theta}) $ 替代 $ X_{1}(e^{j\theta}) $，并利用 $ \hat{X}_{1}(e^{j\theta}) $ 在 $ \left|\theta\right| > \pi $ 为零，就有

$$
\begin{aligned}{X(\mathrm{e}^{\mathrm{j}\omega})=}&{{}\frac{1}{2\pi}\int_{-\pi}^{\pi}\hat{\vec{X}}_{1}(\mathrm{e}^{\mathrm{j}\theta})X_{2}(\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta}\\ {=}&{{}\frac{1}{2\pi}\int_{-\infty}^{\infty}\hat{\vec{X}}_{1}(\mathrm{e}^{\mathrm{j}\theta})X_{2}(\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta}\\ \end{aligned}
$$

因此， $ X(e^{j\omega}) $ 是矩形脉冲 $ \hat{X}(e^{j\omega}) $ 和周期方波 $ X_{2}(e^{j\omega}) $ 的非周期卷积的 $ 1/2\pi $ 倍， $ \hat{X}_{1}(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $ 如图 5.19 所示。这一卷积的结果就是傅里叶变换 $ X(e^{j\omega}) $，如图 5.20 所示。

![图像（物理页 300，第 1 幅）](../Figures/fig-p0300-01.jpg){#fig:p300-1}

**图 5.19 代表 $ X_{1}(e^{j\omega}) $ 一个周期的 $ X(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $。 $ \hat{X}(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $ 的线性卷积就相应于 $ X_{1}(e^{j\omega}) $ 和 $ X_{2}(e^{j\omega}) $ 的周期卷积。**

![图像（物理页 300，第 2 幅）](../Figures/fig-p0300-02.jpg){#fig:p300-2}

**图 5.20 例 5.15 周期卷积的结果**

### 5.6 傅里叶变换性质和基本傅里叶变换对列表 {#sec:5-6}

表5.1综合了离散时间傅里叶变换的若干重要性质，并指出在正文中讨论它们的节次。

表5.2汇总了一些基本而最重要的离散时间傅里叶变换对，其中大多数在正文的例子中都曾导出过。

Table: 表5.1 傅里叶变换性质 {#tbl:5-1}

| 节次 | 性质 | 非周期信号 | 傅里叶变换 |
| --- | --- | --- | --- |
|  |  | x[n] | $ X(e^{j\omega}) $ |
|  |  | y[n] | $ Y(e^{j\omega}) $ |
| 5.3.2 | 线性 | $ ax[n]+by[n] $ | $ aX(e^{j\omega})+bY(e^{j\omega}) $ |
| 5.3.3 | 时移 | $ x[n-n_0] $ | $ e^{-j\omega\pi_0}X(e^{j\omega}) $ |
| 5.3.3 | 频移 | $ e^{j\omega_0n}x[n] $ | $ X(e^{j(\omega-\omega_0)}) $ |
| 5.3.4 | 共轭 | $ x^*[n] $ | $ X^*(e^{-j\omega}) $ |
| 5.3.6 | 时间反转 | x[-n] | $ X(e^{-j\omega}) $ |
| 5.3.7 | 时域扩展 | $ x(k)[n]=\left\{\begin{array}{ll}x[n/k],& \text{若 } n \text{ 为 } k \text{ 的倍数}\\0,&\text{ 若 } n \text{ 不为 } k \text{ 的倍数}\end{array}\right. $ | $ X(e^{j\omega}) $ |
| 5.4 | 卷积 | $ x[n] * y^-\cdot n] $ | $ X(e^{j\omega})Y(e^{j\omega}) $ |
| 5.5 | 相乘 | $ x[n]y[n] $ | $ \frac{1}{2\pi}\int_{2\pi}X(e^{j\theta})Y(e^{j(\omega-\theta)})\mathrm{d}\theta $ |
| 5.3.5 | 时域差分 | $ x[n]-x[n-1] $ | $ (1-e^{-j\omega})X(e^{j\omega}) $ |
| 5.3.5 | 累加 | $ \sum_{k=-\infty}^{n}x[k] $ | $ \frac{1}{1-e^{-j\omega}}X(e^{j\omega}) $ |
|  |  |  | $ + \pi X(e^{j\theta}) \sum_{k=-\infty}^{+\infty} \delta(\omega-2\pi k) $ |
| 5.3.8 | 频域微分 | $ nx[n] $ | $ j\frac{\mathrm{d}X(e^{j\omega})}{\mathrm{d}\omega} $ |
| 5.3.4 | 实信号的共轭对称性 | $ x[n] $为实信号 | $ \begin{cases} X(e^{j\omega}) = X^*(e^{-j\omega}) \\ \mathcal{R}_n\{X(e^{j\omega})\} = \mathcal{R}_n\{X(e^{-j\omega})\} \\ \mathcal{I}_m\{X(e^{j\omega})\} = -\mathcal{I}_m\{X(e^{-j\omega})\} \end{cases} $ |
| 5.3.4 | 实、偶信号的对称性 | $ x[n] $为实、偶信号 | $ X(e^{j\omega}) $实且为偶 |
| 5.3.4 | 实、奇信号的对称性 | $ x[n] $为实、奇信号 | $ X(e^{j\omega}) $纯虚且为奇 |
| 5.3.4 | 实信号的奇偶分解 | $ x_e[n] = \mathcal{E}_n\{x[n]\} $ [x[n]为实] | $ \mathcal{R}_n\{X(e^{j\omega})\} $ |
| 5.3.9 |  | 非周期信号的帕斯瓦尔定理 | $ j\mathcal{I}_m\{X(e^{j\omega})\} $ |
|  | $ \sum_{n=-\infty}^{+\infty} \|x[n]\|^2 = \frac{1}{2\pi}\int_{2\pi} \|X(e^{j\omega})\|^2\mathrm{d}\omega $ |  |  |

| 信号 | 傅里叶变换 | 傅里叶级数系数(若为周期的) |
| --- | --- | --- |
| $ \sum_{k=(N)}^{1}a_{k}\hat{e}^{jk(2\pi/N)n} $ | $ 2\pi\sum_{k=-\infty}^{+\infty}a_{k}\delta\left(\omega-\frac{2\pi k}{N}\right) $ | $ a_{k} $ |
| $ \mathrm{e}^{j\omega_{0}\pi} $ | $ 2\pi\sum_{l=-\infty}^{+\infty}\delta(\omega-\omega_{0}-2\pi l) $ | (a) $ \omega_{0}=\frac{2\pi m}{N} $\n $ a_{k}=\begin{cases}1,k=m,m\pm N,m\pm2N,\cdots\\0,其余k\end{cases} $\n(b) $ \frac{\omega_{0}}{2\pi} $ 无理数 $ \Rightarrow $信号是非周期的 |
| $ \cos\omega_{0}n $ | $ \pi\sum_{l=-\infty}^{+\infty}\{\delta(\omega-\omega_{0}-2\pi l)+\delta(\omega+\omega_{0}-2\pi l)\} $ | (a) $ \omega_{0}=\frac{2\pi m}{N} $\n $ a_{k}=\begin{cases}\frac{1}{2},k=\pm m,\pm m\pm N,\pm m\pm2N,\cdots\\0,其余k\end{cases} $\n(b) $ \frac{\omega_{0}}{2\pi} $ 无理数 $ \Rightarrow $信号是非周期的 |
| $ \sin\omega_{0}n $ | $ \frac{\pi}{j}\sum_{l=-\infty}^{+\infty}\|\delta(\omega-\omega_{0}-2\pi l)-\delta(\omega-\omega_{0}-2\pi l)\| $ | (a) $ \omega_{0}=\frac{2\pi r}{N} $\n $ a_{k}=\begin{cases}\frac{1}{2j},k=r,r\pm N,r\pm2N,\cdots\\-\frac{1}{2j},k=-r,-r\pm N,-r\pm2N,\cdots\\0,其余k\end{cases} $\n(b) $ \frac{\omega_{0}}{2\pi} $ 无理数 $ \Rightarrow $信号是非周期的 |
| x[n]=1 | $ 2\pi\sum_{l=-\infty}^{+\infty}\delta(\omega-2\pi l) $ | $ a_{k}=\begin{cases}1,k=0,\pm N,\pm2N,\cdots\\0,其余k\end{cases} $ |
| 周期方波\n $ x[n]=\begin{cases}1,&\|n\|\leq N_{1}\\0,&N_{1}<\|n\|\leq N/2\end{cases} $ 和\n $ x[n+N]=x[n] $ | $ 2\pi\sum_{k=-\infty}^{+\infty}a_{k}\delta\left(\omega-\frac{2\pi k}{N}\right) $ | $ a_{k}=\frac{\sin[(2\pi k/N)(N_{1}+\frac{1}{2})]}{N\sin[2\pi k/2N]}, $\n $ k\neq0,\pm N,\pm2N,\cdots $\n $ a_{k}=\frac{2N_{1}+1}{N},k=0,\pm N,\pm2N,\cdots $ |
| $ \sum_{k=-\infty}^{+\infty}\delta[n-kN] $ | $ \frac{2\pi}{N}\sum_{k=-\infty}^{+\infty}\delta\left(\omega-\frac{2\pi k}{N}\right) $ | $ a_{k}=\frac{1}{N} $对全部k |
| $ a^{n}u[n],\|a\|<1 $ | $ \frac{1}{1-ae^{-j\omega}} $ | — |
| $ x[n]\begin{cases}1,&\|n\|\leq N_{1}\\0,&\|n\|>N_{1}\end{cases} $ | $ \frac{\sin[\omega(N_{1}+\frac{1}{2})]}{\sin(\omega/2)} $ | — |
| $ \frac{\sin W_{n}}{\pi n}=\frac{W}{\pi}\sin c\left(\frac{W_{n}}{\pi}\right) $\n $ 0<W<\pi $ | $ X(\omega)=\begin{cases}1,&0\leq\|\omega\|\leq W\\0,&W<\|\omega\|\leq\pi\end{cases} $\n $ X(\omega) $周期的，周期为 $ 2\pi $ | — |
| $ \delta[n] $ | 1 | — |

续表5.2

| 信号 | 傅里叶变换 | 傅里叶级数系数(若为周期的) |
| --- | --- | --- |
| u[n] | $ \frac{1}{1 - e^{-j\omega}} + \sum_{k=-\infty}^{+\infty} \pi \delta(\omega - 2\pi k) $ | — |
| $ \delta[n-n_0] $ | $ e^{-j\omega n_0} $ | — |
| (n+1)a^n u[n], \|a\|<1 | $ \frac{1}{(1-a e^{-j\omega})^2} $ | — |
| $ \frac{(n+r-1)!}{n!(r-1)!}a^n u[n]<1 $ | $ \frac{1}{(1-a e^{-j\omega})^r} $ | — |

### 5.7 对偶性 {#sec:5-7}

在讨论连续时间傅里叶变换中，已经观察到在分析公式(4.9)式和综合公式(4.8)式之间有某种对称性或对偶性存在，然而对离散时间傅里叶变换而言，分析公式(5.9)式和综合公式(5.8)式之间却不存在相应的对偶性。但是，在离散时间傅里叶级数公式(3.94)式和(3.95)式之间却存在一种对偶关系，这将在5.7.1节进行讨论。另外，在离散时间傅里叶变换和连续时间傅里叶级数之间也存在一种对偶关系，这一关系将在5.7.2节讨论。

#### 5.7.1 离散时间傅里叶级数的对偶性 {#sec:5-7-1}

因为一个周期信号 $ x[n] $ 的傅里叶级数系数 $ a_{k} $ 本身就是一个周期序列，我们就能将这个序列 $ a_{k} $ 展开成傅里叶级数。离散时间傅里叶级数的对偶性质意味着周期序列 $ a_{k} $ 的傅里叶级数系数是 $ \left(\frac{1}{N}x[-n]\right) $ 的值（也就是说正比于原信号在时间反转后的值）。为了更仔细地看出这一点，现考虑两个周期均为 N 的周期序列，这两个序列通过下列和式联系起来

$$
f[m]=\frac{1}{N}\sum_{r=(N)}g[r]\dot{\mathrm{e}}^{-\mathrm{j}r(2\pi/N)m}
$$

如果令 m=k 和 r=n，则(5.65)式就变成

$$
f[k]=\frac{1}{N}\sum_{n=(N)}g[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n}
$$

将该式与(3.95)式比较可知，序列 $ f[k] $ 就相应于信号 g[n] 的傅里叶级数系数，也就是说，如果对一个周期离散时间信号和它的傅里叶级数系数采用在第 3 章所引入的符号

$$
x[n]^{\mathcal{P S}}\leftrightarrow a_{k}
$$

那么，通过(5.65)式相联系的两个周期序列就满足

$$
g[n]{\overset{\mathcal{P S}}{\leftrightarrow}}f[k]
$$

另一方面，若令 m=n 和 r=-k，则(5.65)式就变为

$$
f[n]=\sum_{k=(N)}\frac{1}{N}g[-k]e^{j k(2\pi/N)n}
$$

将该式与(3.94)式比较可知， $ (1/N)g[-k] $就相应于 $ f[n] $的傅里叶级数的系数序列，即

$$
f[n]\overset{\mathcal{A S}}{\leftrightarrow}\frac{1}{N}g[-k]
$$

和连续时间情况一样，这一对偶性意味着：离散时间傅里叶级数的每一个性质都有其对应的一个对偶关系存在。例如，参照表3.2，如下一对性质就是对偶的：

$$
x\left[n-n_{0}\right]\overset{\mathcal{F}S}{\leftrightarrow}a_{k}\mathrm{e}^{-\mathrm{i}k\left(2\pi/N\right)n_{0}}
$$

和

$$
\mathrm{e}^{\mathrm{j}m\left(2\pi/N\right)n}x\left[n\right]^{\mathcal{P}S}\leftrightarrow a_{k-m}
$$

同理，从该表上可以提取的另一对对偶关系如下：

$$
\sum_{r=(N)}x[r]y[n-r]^{\mathcal{I S}}\leftrightarrow\mathsf{N a}_{k}b_{k}
$$

和

$$
x[n]y[n]\overset{\mathcal{F S}}{\leftrightarrow}\sum_{l=(N)}a_{l}b_{k-l}
$$

对于离散时间傅里叶级数的性质除了上述结果以外，对偶性还常常用以简化涉及求取傅里叶级数表示式的复杂计算上。这点将用如下例子给予说明。

例 5.16 考虑周期为 N=9 的下面周期信号：

$$
x[n]=\left\{\begin{aligned}&\frac{1}{9}\ \frac{\sin(5\pi n/9)}{\sin(\pi n/9)},\quad&k\neq9 的倍数 \\ &\frac{5}{9},\quad&k=9 的倍数 \end{aligned}\right.
$$

在第3章，曾求得一个矩形方波的傅里叶系数在形式上与(5.72)式很相像。由对偶性使人想到， $ x[n] $的傅里叶系数也一定具有矩形方波的形式。为了更仔细地看出这点，令 $ g[n] $是一个周期为N=9的周期方波，而有

$$
g[n]=\left\{\begin{aligned}&1,~\mid~n~\mid\leqslant2\\ &0,~2<|\begin{matrix}n\end{matrix}|\leqslant4\end{aligned}\right.
$$

$ g[n] $的傅里叶级数系数 $ b_{k} $可由例3.12确定为

$$
b_{k}=\left\{\begin{aligned}&\frac{1}{9}\frac{\sin(5\pi k/9)}{\sin(\pi k/9)},&\quad&n\neq9 的倍数 \\ &\frac{5}{9},&\quad&n=9 的倍数 \end{aligned}\right.
$$

对于 $ g[n] $ 的傅里叶级数分析公式 (3.95) 式，现在可以写成

$$
b_{k}=\frac{1}{9}\sum_{n=-2}^{2}(1)\mathrm{e}^{-\mathrm{j}2\pi\mathrm{i}k/9}
$$

将变量 k 和 n 的名称互换，并将 $ x[n]=b_{k} $，求得

$$
x[n]=\frac{1}{9}\sum_{k=-2}^{2}(1)\mathrm{e}^{-\mathrm{j}2\pi n k/9}
$$

再在右边和式中令 $ k' = -k $，得到

$$
x_{-}^{[}n]=\frac{1}{9}\sum_{k^{^{\prime}}=-2}^{2}\mathrm{e}^{+j2\pi n k^{^{\prime}}/9}
$$

最后，将因子1/9移至求和号里面，可见这个式子的右边就具有对x[n]的综合公式(3.94)式的形式，据此得出x[n]的傅里叶系数就是

$$
a_{k}=\left\{\begin{aligned}&1/9,\mid k\mid\leqslant2\\ &0,\quad2<\mid k\mid\leqslant4\end{aligned}\right.
$$

当然这是周期的，周期 N=9。

#### 5.7.2 离散时间傅里叶变换和连续时间傅里叶级数之间的对偶性 {#sec:5-7-2}

除了离散时间傅里叶级数的对偶性以外，在离散时间傅里叶变换和连续时间傅里叶级数之间也存在着一种对偶关系。现在让我们将连续时间傅里叶级数公式(3.38)式和(3.39)式与离散时间傅里叶变换公式(5.8)式和(5.9)式作一比较。为方便起见，将这些公式重新写出如下：

$$
x[n]=\frac{1}{2\pi}\int_{2\pi}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega
$$

$$
X(e^{j\omega})=\sum_{n=-\infty}^{+\infty}x[n]e^{-j\omega n}
$$

$$
x(t)=\sum_{k=-\infty}^{+\infty}a_{k}\mathrm{e}^{\mathrm{j}k\omega_{0}t}
$$

$$
a_{k}=\frac{1}{T}\int_{T}x(t)\mathrm{e}^{-\mathrm{j}k w_{0}t}\mathrm{d}t
$$

可以注意到，(5.73)式和(5.76)式是很相像的，(5.74)式和(5.75)式也是很类似的。事实上，可以将(5.73)式和(5.74)式看作周期性频率响应 $ X(e^{j\omega}) $ 的傅里叶级数表示。特别是，因为 $ X(e^{j\omega}) $ 是 $ \omega $ 的周期函数，周期为 $ 2\pi $，它就有一个用成谐波关系的周期指数函数的加权和的傅里叶级数表示，所有这些成谐波关系的周期指数函数都有一个公共周期为 $ 2\pi $。这也就是说， $ X(e^{j\omega}) $ 能够表示成信号 $ e^{j\omega m} $， $ n=0,\pm1,\pm2,\cdots $ 的加权和的傅里叶级数。由(5.74)式可见，在这个展开式中的第 $ n $ 次傅里叶系数（也即与 $ e^{j\omega m} $ 相乘的系数）是 $ x[-n] $。再者，因为 $ X(e^{j\omega}) $ 的周期是 $ 2\pi $，所以(5.73)式也就能够看作是对傅里叶级数系数 $ x[n] $ 的傅里叶级数的分析公式，也就是在(5.74)对 $ X(e^{j\omega}) $ 的表示式中与 $ e^{-j\omega m} $ 相乘的系数。这一对偶关系的应用最好用一个例子来说明。

例 5.17 可以利用离散时间傅里叶变换综合公式和连续时间傅里叶级数分析公式之间的对偶性来求下面序列的离散时间傅里叶变换：

$$
x[n]=\frac{\sin(\pi n/2)}{\pi n}
$$

为了利用对偶性，首先就必须要确认一个周期 $ T=2\pi $ 的连续时间信号 $ g(t) $，其傅里叶系数 $ a_{k}=x[k] $。由例3.5知道， $ g(t) $ 是一个周期为 $ 2\pi $（或者等效为基波频率 $ \omega_{0}=1 $）的周期性方波为

$$
g(t)=\left\{\begin{aligned}{1,}&{{}\mid t\mid\leqslant T_{1}}\\ {0,}&{{}\;T_{1}<\mid t\mid\leqslant\pi}\\ \end{aligned}\right.
$$

那么， $ g(t) $的傅里叶级数系数是

$$
a_{k}=\frac{\sin(k T_{1})}{k\pi}
$$

这样，若取 $ T_{1}=\pi/2 $，就有 $ a_{k}=x[k] $。这时， $ g(t) $ 的分析公式是

$$
\frac{\sin(\pi k/2)}{\pi k}=\frac{1}{2\pi}\int_{-\pi}^{\pi}g(t)\mathrm{e}^{-\mathrm{i}kt}\mathrm{d}t=\frac{1}{2\pi}\int_{-\pi/2}^{\pi/2}(1)\mathrm{e}^{-\mathrm{i}kt}\mathrm{d}t
$$

将 k 写为 n, t 写为 $ \omega $, 则有

$$
\frac{\sin(\pi n/2)}{\pi n}=\frac{1}{2\pi}\int_{-\pi/2}^{\pi/2}(1)\mathrm{e}^{-\mathrm{i}n\omega}\mathrm{d}\omega
$$

在上式两边以 -n 代换 n，并注意到 $ \mathrm{sinc} $ 函数是偶函数，得出

$$
\frac{\sin(\pi n/2)}{\pi n}=\frac{1}{2\pi}\int_{-\pi/2}^{\pi/2}(1)\mathrm{e}^{\mathrm{j}n\omega}\mathrm{d}\omega
$$

上式的右边具有对 x[n] 的傅里叶变换综合公式的形式，这里

$$
X(\mathrm{e}^{\mathrm{i}\omega})=\left\{\begin{aligned}&1&|\omega|\leqslant&\pi/2\\ &0&\pi/2<|\omega|\leqslant&\pi\end{aligned}\right.
$$

表5.3 简要地综合了连续和离散时间信号的傅里叶级数和傅里叶变换表示式，同时也指出了每一种情况下的对偶关系。

Table: 表5.3 傅里叶级数与傅里叶变换综合 {#tbl:5-3}

|  | 连续时间 | 离散时间 |  |  |
| --- | --- | --- | --- | --- |
| 时域 | 频域 | 时域 | 频域 |  |
| 傅里叶级数 | $ x(t)=\sum_{k=-\infty}^{+\infty}a_k\mathrm{e}^{\mathrm{j}k\omega_0t} $连续时间，在时间上是周期的 | $ a_k=\frac{1}{T_0}\int_{T_0}^{T}x(t)\mathrm{e}^{-\mathrm{j}k\omega_0t}\mathrm{d}t $离散频率，在频率上是非周期的 | $ x[n]=\sum_{k=(N)!}^{}a_k\mathrm{e}^{\mathrm{j}k(2\pi/N)n} $离散时间，在时间上是周期的 | $ a_k=\frac{1}{N}\sum_{n=(N)}^{}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n} $离散频率，在频率上是周期的 |
| 傅里叶变换 | $ x(t)=\frac{1}{2\pi}\int_{-\infty}^{+\infty}X(\mathrm{j}\omega)\mathrm{e}^{\mathrm{j}\omega t}\mathrm{d}t $连续时间，在时间上是非周期的\n←对偶→ | $ X(\mathrm{j}\omega)=\int_{-\infty}^{+\infty}x(t)\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t $连续频率，在频率上是非周期的 | 偶 $ \searrow $\n $ x[n]=\frac{1}{2\pi}\int_{2\pi}^{2N}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega n}\mathrm{d}\omega $\n离散时间，在时间上是非周期的 | $ X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{n=-\infty}^{+\infty}x[n]\mathrm{e}^{-\mathrm{j}\omega n} $连续频率，在频率上是周期的 |

### 5.8 由线性常系数差分方程表征的系统 {#sec:5-8}

对一个 LTI 系统而言，其输出 y[n] 和输入 x[n] 间的线性常系数差分方程一般具有如下形式：

$$
\sum_{k=0}^{N}a_{k}y[{\bf\Gamma n}-{\bf\Gamma k}]={\bf\Gamma}\sum_{k=0}^{M}b_{k}x[{\bf\Gamma n}-{\bf\Gamma k}]
$$

由这样的差分方程所描述的系统是十分重要而有用的一类系统。这一节将利用离散时间傅里叶变换的几个性质导出由这样一个方程所描述的LTI系统的频率响应 $ H(e^{j\omega}) $。所采用的方法是与4.7节讨论由线性常系数微分方程所描述的连续时间LTI系统时紧密并行的。

有两种方法来确定 $ H(e^{j\omega}) $。其中的第一种是曾在 3.11 节对几个简单的差分方程所说明的，这就是利用复指数是 LTI 系统特征函数这一事实来求。若 $ x[n] = e^{j\omega n} $ 是一个 LTI 系统的输入，那么其输出就一定具有 $ H(e^{j\omega}) e^{j\omega n} $ 这种形式。将这些表达式代入 (5.78) 式，并做一些代数运算就可以解出 $ H(e^{j\omega}) $。这一节，将采用第二种途径，利用离散时间傅里叶变换的卷

积、线性和时移性质来求。设 $ X(e^{j\omega}) $、 $ Y(e^{j\omega}) $ 和 $ H(e^{j\omega}) $ 分别为输入 $ X[n] $、输入 $ y[n] $ 和单位脉冲响应 $ h[n] $ 的傅里叶变换，那么离散时间傅里叶变换的卷积性质就意味着有

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{Y(\mathrm{e}^{\mathrm{j}\omega})}{X(\mathrm{e}^{\mathrm{j}\omega})}
$$

在(5.78)式两边应用傅里叶变换，并利用线性和时移性质，就得

$$
\sum_{k=0}^{N}a_{k}\mathrm{e}^{-\mathrm{j}k\omega}Y(\mathrm{e}^{\mathrm{j}\omega})=\sum_{k=0}^{M}b_{k}\mathrm{e}^{-\mathrm{j}k\omega}X(\mathrm{e}^{\mathrm{j}\omega})
$$

或者等效为

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{Y(\mathrm{e}^{\mathrm{j}\omega})}{X(\mathrm{e}^{\mathrm{j}\omega})}=\frac{\sum_{k=0}^{M}b_{k}\mathrm{e}^{-\mathrm{j}k\omega}}{\sum_{k=0}^{N}a_{k}\mathrm{e}^{-\mathrm{j}k\omega}}
$$

将(5.80)式与(4.76)式作一比较可见，像在连续时间情况下一样， $ H(e^{j\omega}) $是两个多项式的比，但是在离散时间下，这些多项式的变量是 $ e^{-j\omega} $。分子多项式的系数就是出现在(5.78)式右边的系数，而分母多项式的系数就是(5.78)式左边的系数。因此，由(5.78)式表征的LTI系统的频率响应就能够凭直观写出来。

(5.78)式的差分方程一般就称为N阶差分方程，因为它涉及输出 $ y[n] $直到N步的延迟。同时(5.80)式 $ H(e^{j\omega}) $的分母也是以 $ e^{-j\omega} $的N阶多项式。

例 5.18 考虑一因果 LTI 系统，其差分方程为

$$
y[n]-a y[n-1]=x[n]
$$

其中 $ |a|<1 $。由(5.80)式，该系统的频率响应是

$$
H(e^{\mathrm{j}\omega})=\frac{1}{1-a e^{-\mathrm{j}\omega}}
$$

将(5.82)式与例5.1比较可知，它就是序列 $ a^{n}u[n] $的傅里叶变换。因此，该系统的单位脉冲响应是

$$
h[n]=a^{n} u[n]
$$

例 5.19 考虑一因果 LTI 系统，其差分方程为

$$
y[n]-\frac{3}{4}y[n-1]+\frac{1}{8}y[n-2]=2x[n]
$$

由(5.80)式，频率响应是

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{2}{1-\frac{3}{4}\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{8}\mathrm{e}^{-\mathrm{j}2\omega}}
$$

为求单位脉冲响应，第一步是要将(5.85)式的分母因式分解为：

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{2}{(1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega})(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})}
$$

$ H(e^{jw}) $就能按部分分式展开，如同附录中例A.3那样，展开的结果为

$$
H(\mathrm{e}^{\mathrm{j}\omega})\frac{4}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}-\frac{2}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}
$$

式中每一项的反变换都可凭直观写出，其结果为

$$
h[n]=4\Bigl(\frac{1}{2}\Bigr)^{n}u[n]-2\Bigl(\frac{1}{4}\Bigr)^{n}u[n]
$$

在例 5.19 中所采用的步骤与在连续时间情况下所用的是相同的，这就是：在将 $ H(e^{\omega}) $ 利用部分分式方法展开以后，就能凭直观求得每一项的反变换。这一方法可用于由线性常系数差分方程所描述的任何 LTI 系统的频率响应，以确定该系统的单位脉冲响应。同时，如同在下面这个例子所说明的，若这样的系统输入的傅里叶变换 $ X(e^{\omega}) $ 也是一个以 $ e^{-j\omega} $ 的多项式之比，那么 $ Y(e^{\omega}) $ 也一定是 $ e^{-j\omega} $ 的多项式之比。这时可用同样的办法求得系统对输入 $ x[n] $ 的响应 $ y[n] $。

**例 5.20 考虑例 5.19 的 LTI 系统，并设系统输入为**

$$
x[n]=\left(\frac{1}{4}\right)^{n} u[n]
$$

利用(5.80)式和例5.1或例5.18，可得

$$
\begin{aligned}{Y(\mathrm{e}^{\mathrm{j}\omega})=H(\mathrm{e}^{\mathrm{j}\omega})X(\mathrm{e}^{\mathrm{j}\omega})=}&{{}\left[\frac{2}{(1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega})(\mathrm{1}-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})}\right]\left[\frac{1}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}\right]}\\ {=}&{{}\frac{2}{(1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega})(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})^{2}}}\\ \end{aligned}
$$

如同在附录中给出的，这种情况下的部分分式展开式是

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\frac{B_{11}}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}+\frac{B_{12}}{(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})^{2}}+\frac{B_{21}}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}
$$

式中常数 $ B_{11} $、 $ B_{12} $ 和 $ B_{21} $ 可用附录中给出的方法求出。这个特定的展开式在附录例 A.4 中详细地列出来了，所得到的值是

$$
B_{11}=-4,\;B_{12}=-2,\;B_{21}=8
$$

这样

$$
Y(e^{\mathrm{j}\omega})=-\frac{4}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}-\frac{2}{(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})^{2}}+\frac{8}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}
$$

上式第一和第三项与在例5.19中所遇到的形式相同，而第二项与在例5.13中所见过的一样。无论由这些例子，还是根据表5.2，都能将(5.91)式中的每一项求反变换，而得出

$$
y[n]=\left\{-4\Big(\frac{1}{4}\Big)^{n}-2(n+1)\Big(\frac{1}{4}\Big)^{n}+8\Big(\frac{1}{2}\Big)^{n}\right\}u[n]
$$

### 5.9 小结 {#sec:5-9}

这一章和第4章相并行地研究了离散时间信号的傅里叶变换，并考察了它的许多重要性质。贯穿整个这一章，已经看到连续时间和离散时间傅里叶分析之间有很多类似之处，同时也看到了某些重要的差别。例如，在离散时间情况下，傅里叶级数和傅里叶变换之间的关系是非常类似于在连续时间情况下两者之间的关系的。尤其是，由离散时间傅里叶级数表示导出非周期信号的离散时间傅里叶变换的过程与在连续时间情况下所对应的几乎是完全一样的。再者，连续时间傅里叶变换的很多性质都能在离散时间情况下找到相对应的性质。但另

一方面，与连续时间情况相比，一个非周期信号的离散时间傅里叶变换则总是周期的，且周期为 $ 2\pi $。除了上述这些异同点之外，还讨论了连续时间和离散时间信号的傅里叶表示之间的对偶关系。

连续时间和离散时间傅里叶分析之间最重要的类同之处还在于它们在分析和表示信号以及在LTI系统中的应用。更具体一点，就是卷积性质提供了LTI系统频域分析的基础。我们已经看到了这一途径在第3到第5章滤波问题的讨论以及在研究由线性常系数微分及差分方程所描述的系统中的某些应用。并且，在第6章更详细地研究滤波和时域与频域的关系问题中，将会对此有更进一步的体会。另外，连续时间和离散时间中的相乘性质则是第7章研究采样和第8章讨论通信系统问题的基础。

**习题**

习题的第一部分属于基本题，答案在书末给出。其余三个部分属于基本题、深入题和扩充题。

**基本题（附答案）**

5.1 利用傅里叶变换分析公式(5.9)式，计算下列傅里叶变换：

(a) $ \left(\frac{1}{2}\right)^{n-1}u[n-1] $ (b) $ \left(\frac{1}{2}\right)^{|n-1|} $

概略画出每一傅里叶变换在一个周期内的模，并给以标注。

5.2 利用傅里叶变换分析公式(5.9)式，计算下列傅里叶变换：

(a) $ \delta[n-1]+\delta[n+1] $ (b) $ \delta[n+2]-\delta[n-2] $

概略画出每一傅里叶变换在一个周期内的模，并给以标注。

5.3 对于 $ -\pi \leqslant \omega < \pi $，求下列周期信号的傅里叶变换：

(a) $ \sin\left(\frac{\pi}{3}n+\frac{\pi}{4}\right) $ (b) $ 2+\cos\left(\frac{\pi}{6}n+\frac{\pi}{8}\right) $

5.4 利用傅里叶变换的综合公式(5.8)式求下列反变换：

$$
\mathrm{a)}X_{1}(\mathrm{e}^{\mathrm{j}\omega})=\sum_{k=-\infty}^{\infty}\left\{2\pi\delta(\omega-2\pi k)+\pi\delta(\omega-\frac{\pi}{2}-2\pi k)+\pi\delta(\omega+\frac{\pi}{2}-2\pi k)\right\}
$$

$$
X_{2}(\mathrm{e}^{\mathrm{i}\omega})=\left\{\begin{aligned}&2\mathrm{j},&&0<\omega\leqslant\pi\\ &-2\mathrm{j},&&-\pi<\omega\leqslant0\end{aligned}\right.
$$

5.5 利用傅里叶变的综合公式(5.8)式，求 $ X(e^{j\omega}) = |X(e^{j\omega})| e^{j k X(e^{j\omega})} $ 的反变换，其中

$$
\mid X(\mathrm{e}^{\mathrm{j}\omega})\mid=\left\{\begin{aligned}&1,0\leqslant|\omega|<\frac{\pi}{4}\\ &0,\frac{\pi}{4}\leqslant|\omega|\leqslant\pi\end{aligned}\right.,\quad\rightleftharpoons X(\mathrm{e}^{\mathrm{j}\omega})=-\frac{3\omega}{2}
$$

根据答案求 $ x[n]=0 $ 时的 n 值。

5.6 已知 $ x[n] $ 有傅里叶变换 $ X(e^{jw}) $，用 $ X(e^{jw}) $ 表示下列信号的傅里叶变换。可以利用表 5.1 的傅里叶变换性质来做。

(a) $ x_{1}[n]=x[1-n]+x[-1-n] $ (b) $ x_{2}[n]=\frac{x^{*}[-n]+x[n]}{2} $ (c) $ x[-n]=(n-1)^{2}-[-n] $

5.7 对于下面每一傅里叶变换，利用傅里叶变换性质(表5.1)，确定是否对应的时域信号是(i)实、虚信号，或均不是；(ii)偶、奇信号，或均不是。解本题时勿需求出任何反变换。

(a) $ X_1(e^{j\omega}) = e^{-j\omega} \sum_{k=1}^{10} (\sin k\omega) $ (b) $ X_2(e^{j\omega}) = j \sin(\omega) \cos(5\omega) $

(c) $ \mathrm{X}_{3}(\mathrm{e}^{\mathrm{j}\omega}) = A(\omega) + \mathrm{e}^{\mathrm{j}B(\omega)} $，其中

$$
A\left(\omega\right)=\left\{\begin{aligned}{}&{{}1,\;0\leqslant|\omega|\leqslant\frac{\pi}{8}}\\ {}&{{}0,\;\frac{\pi}{8}<|\omega|\leqslant\pi}\\ \end{aligned}\right.;\quad B\left(\omega\right)=-\frac{3\omega}{2}+\pi
$$

5.8 借助于表5.1和表5.2，当 $ X(e^{j\omega}) $为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{1-\mathrm{e}^{-\mathrm{j}\omega}}\left[\frac{\sin\frac{3}{2}\omega}{\sin\frac{\omega}{2}}\right]+5\pi\delta(\omega),-\pi<\omega\leqslant\pi.
$$

求 $ x[n]_{0} $

5.9 对某一特殊的 x[n]，其傅里叶变换为 $ X(e^{j\omega}) $，已知下面四个条件

1. $ x[n] = 0 $, n > 0

2.x[0]>0

3. $ \mathcal{A}_m\{X(\mathrm{e}^{\mathrm{j}\omega})\} = \sin\omega - \sin2\omega $

4. $ \frac{1}{2\pi}\int_{-\pi}^{\pi}|x(e^{j\omega})|^{2}d\omega=3 $

求 $ x[n] $。

5.10 利用表5.1和表5.2，并结合

$$
X(e^{j\theta})=\sum_{n=-\infty}^{\infty}x[n]
$$

确定

$$
A=\sum_{n=0}^{\infty}n\left(\frac{1}{2}\right)^{n}
$$

的数值。

5.11 考虑一信号 $ g[n] $，其傅里叶变换为 $ G(e^{j\omega}) $，假设

$$
g[n]=x_{(2)}[n]
$$

这里信号 x[n] 的傅里叶变换为 $ X(e^{j\omega}) $。试确定某一实数 a， $ 0 < \alpha < 2\pi $，并有 $ G(e^{j\omega}) = G(e^{j(\omega - \alpha)}) $。

5.12 设

$$
y[n]=\left(\frac{\sin\frac{\pi}{4}n}{\pi n}\right)^{2}*\left(\frac{\sin\omega_{c}n}{\pi n}\right)
$$

式中 * 记为卷积，且 $ \left|\omega_{c}\right|\leqslant\pi $。试对 $ \omega_{c} $ 确定一个较严格的限制，以保证

$$
y[n]=\left(\frac{\sin\frac{\pi}{4}n}{\pi n}\right)^{2}
$$

5.13 一单位脉冲响应 $ h_{1}[n]=\left(\frac{1}{3}\right)^{n}u[n] $ 的 LTI 系统与另一单位脉冲响应为 $ h_{2}[n] $ 的因果 LTI 系统并联联结，并联后的频率响应为

$$
H(\mathrm{e}^{\mathrm{j}\omega})=\frac{-12+5\mathrm{e}^{-\mathrm{j}\omega}}{12-7\mathrm{e}^{-\mathrm{j}\omega}+\mathrm{e}^{-\mathrm{j}2\omega}}
$$

求 $ h_{2}[n] $。

5.14 假设一单位脉冲响应为 $ h[n] $，频率响应为 $ H(e^{j\omega}) $ 的 LTI 系统 S，具有下列条件：

1. $ (\frac{1}{4})^{n}u[n] \to g[n] $，其中 $ g[n] = 0 $， $ n \geqslant 2 $ 和 n < 0

$$
2.H(\mathrm{e}^{\mathrm{j}\pi/2})=1
$$

$$
3.H(\mathrm{e}^{\mathrm{j}\omega})=H(\mathrm{e}^{\mathrm{j}(\alpha-\pi)})
$$

求 $ h[n] $。

### 5.15 设 $ Y(e^{j\omega}) $ 的反变换是 {#sec:5-15}

$$
y[n]=\left(\frac{\sin\omega_{c}n}{\pi n}\right)^{2}
$$

其中 $ 0<\omega_{c}<\pi $ 。试确定 $ \omega_{c} $ 的值，以保证

$$
Y(e^{i\pi})=\frac{1}{2}
$$

### 5.16 有一信号的傅里叶变换是 {#sec:5-16}

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\sum_{k=0}^{3}\frac{(1/2)^{k}}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}(\omega-\pi/2)k}}
$$

可以证明

$$
x[n]=g[n]q[n]
$$

其中 $ g[n] $ 具有 $ a^{n}u[n] $ 形式， $ q[n] $ 是周期为 N 的周期信号。

(a) 求 $ \alpha $ 的值。 (b) 求 N 的值。 (c) x[n] 是实序列吗？

5.17 信号 $ x[n]=(-1)^{n} $ 有一基波周期为2，傅里叶级数系数为 $ a_{k} $，利用对偶性求基波周期为2的信号 $ g[n]=a_{n} $ 的傅里叶级数系数 $ b_{k} $。

5.18 已知

$$
a^{\left|n\right|}\xrightarrow{\mathcal{S}}\frac{1-a^{2}}{1-2a\cos\omega+a^{2}},\mid a\mid<1
$$

利用对偶性求下面周期 T=1 的连续时间信号的傅里叶级数系数：

$$
x(t)=\frac{1}{5-4\cos(2\pi t)}
$$

5.19 考虑一因果稳定的 LTI 系统 S，其输入 x[n] 和输出 y[n] 通过下面二阶差分方程所关联：

$$
y[n]-\frac{1}{6}y[n-1]-\frac{1}{6}y[n-2]=x[n]
$$

(a) 求该系统 S 的频率响应 $ H(e^{j\omega}) $

(b) 求系统 S 的单位脉冲响应 $ h[n] $

5.20 有一因果稳定的 LTI 系统 S，具有下面性质

$$
\left(\frac{4}{5}\right)^{n}u[n]\to n\left(\frac{4}{5}\right)^{n}u[n]
$$

(a) 求该系统的频率响应 $ H(e^{j\omega}) $

(b) 求该系统的差分方程。

**基本题**

5.21 计算下列信号的傅里叶变换：

(a)

$$
x[n]=u[n-2]-u[n-6]
$$

$$
x[n]=(\frac{1}{2})^{-n}u[-n-1]
$$

$$
x[n]=(\frac{1}{3})^{|n|}u[-n-2]
$$

(d) $ x[n]=2^n \sin\left(\frac{\pi}{4}n\right)u[-n] $

(e)

$$
x[n]=(\frac{1}{2})^{|n|}\cos(\frac{\pi}{8}(n-1))
$$

(f) $ x[n] = \left\{ \begin{aligned} n, & -3 \leqslant n \leqslant 3 \\ 0, & \text{其余 } n \end{aligned} \right. $

(g) $ x[n] = \sin\left(\frac{\pi}{2}n\right) + \cos(n) $

$$
x[n]=\sin(\frac{5\pi}{3}n)+\cos(\frac{7\pi}{3}n)
$$

(i) $ x[n] = x[n-6] $ 和 $ x[n] = u[n] - u[n-5] $ $ 0 \leqslant n \leqslant 5 $

$$
x[n]=(n-1)(\frac{1}{3})^{|\pi|}
$$

(k)

$$
x[n]=\left(\frac{\sin(\pi n/5)}{\pi n}\right)\cos(\frac{7\pi}{2}n)
$$

5.22 下列是各离散时间信号的傅里叶变换，求相应于每一变换的信号。

(a) $ X(e^{\mathrm{j}\omega})=\left\{\begin{aligned}&1,&\frac{\pi}{4}\leqslant|\omega|&\leqslant\frac{3\pi}{4}\\ &0,&\frac{3\pi}{4}&\leqslant|\omega|&\leqslant\pi,0\leqslant|\omega|<\frac{\pi}{4}\end{aligned}\right. $

(b) $ X(e^{\mathrm{j}\omega})=1+3e^{-\mathrm{j}\omega}+2e^{-\mathrm{j}2\omega}-4e^{-\mathrm{j}3\omega}+e^{-\mathrm{j}10\omega} $

(c) $ X(e^{j\omega}) = e^{-j\omega/2} $, $ -\pi \leq \omega \leq \pi $

(d) $ X(e^{j\omega}) = \cos^2 \omega + \sin^2 3\omega $

(e) $ X(\mathrm{e}^{\mathrm{j}\omega}) = \sum_{k=-\infty}^{\infty}(-1)^{k}\delta(\omega - \frac{\pi}{2}k) $ (f) $ X(\mathrm{e}^{\mathrm{j}\omega}) = \frac{\mathrm{e}^{-\mathrm{j}\omega} - \frac{1}{5}}{1 - \frac{1}{5}\mathrm{e}^{-\mathrm{j}\omega}} $

(g) $ X(\mathrm{e}^{\mathrm{j}\omega}) = \frac{1 - \frac{1}{3}\mathrm{e}^{-\mathrm{j}\omega}}{1 - \frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega} - \frac{1}{8}\mathrm{e}^{-2\mathrm{j}\omega}} $

(h) $ X(\mathrm{e}^{\mathrm{j}\omega}) = \frac{1 - (\frac{1}{3})^6\mathrm{e}^{-\mathrm{j}6\omega}}{1 - \frac{1}{3}\mathrm{e}^{-\mathrm{j}\omega}} $

5.23 设 $ X(e^{j\omega}) $ 是如图 P5.23 所示的 x[n] 信号的傅里叶变换，不经求出 $ X(e^{j\omega}) $ 完成下列计算：

(a) 求 $ X(e^{j0}) $ (b) 求 $ X(e^{j\omega}) $

(c) 求 $ \int_{-\pi}^{\pi} X(e^{j\omega}) \, d\omega $ (d) 求 $ X(e^{j\pi}) $

(e) 求并画出傅里叶变换为 $ \mathcal{R}_{0}\left\{x\left(\omega\right)\right\} $ 的信号

(f) 求

f) 求

(i) $ \int_{-\pi}^{\pi}|X(e^{j\omega})|^{2}d\omega $ (ii) $ \int_{-\pi}^{\pi}\frac{dX(e^{j\omega})}{d\omega}\bigg|^{2}d\omega $

![图像（物理页 312，第 1 幅）](../Figures/fig-p0312-01.jpg){#fig:p312-1}

**图 P5.23**

5.24 试判定下列各信号，其傅里叶变换有哪一个（如果有）满足下面每一个条件：

1. $ \mathcal{R}_e\{X(e^{j\omega})\} = 0 $

2. $ \mathcal{A}_n\{X(e^{j\omega})\} = 0 $

3. 存在一个实数 $ \alpha $，使得 $ \mathrm{e}^{\mathrm{j}\omega X}(\mathrm{e}^{\mathrm{j}\omega}) $ 为实

4. $ \int_{-\pi}^{\pi} X(e^{j\omega}) \, \mathrm{d}\omega = 0 $

5. $ X(e^{j\omega}) $ 周期的

6. $ X(e^{j0})=0 $

(a) x[n]如图P5.24(a)所示 (b) x[n]如图P5.24(b)所示

(c) $ x[n] = \left(\frac{1}{2}\right)^n u[n] $

(d) $ x[n] = \left(\frac{1}{2}\right)^{|n|} $

(e) $ x[n] = \delta[n - 1] + \delta[n + 2] $

(f) $ x[n] = \delta[n - 1] + \delta[n + 3] $

(g) x[n]如图P5.24(c)所示 (h) x[n]如图P5.24(d)所示

(i) $ x[n] = \delta[n - 1] - \delta[n + 1] $

![图像（物理页 313，第 1 幅）](../Figures/fig-p0313-01.jpg){#fig:p313-1}

**(a)**

![图像（物理页 313，第 2 幅）](../Figures/fig-p0313-02.jpg){#fig:p313-2}

**(b)**

![图像（物理页 313，第 3 幅）](../Figures/fig-p0313-03.jpg){#fig:p313-3}

**(c)**

![图像（物理页 313，第 4 幅）](../Figures/fig-p0313-04.jpg){#fig:p313-4}

**(d)**

**图 P5.24**

5.25 考虑图 P5.25 的信号，设该信号的傅里叶变换用直角坐标写出为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=A(\omega)+\mathrm{j}B(\omega)
$$

试画出对应于变换为

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\left[B(\omega)+A(\omega)\mathrm{e}^{\mathrm{j}\omega}\right]
$$

的时间信号。

5.26 设 $ x_{1}[n] $ 的傅里叶变换 $ X_{1}(e^{j\omega}) $ 如图 P5.26(a) 所示。

(a) 考虑信号 $ x_{2}[n] $，其傅里叶变换 $ X_{2}(e^{j\omega}) $ 如图 P5.26(b) 所示，试用 $ x_{1}[n] $ 来表示 $ x_{2}[n] $

[提示：首先用 $ X_{1}(e^{i\omega}) $ 来表示 $ X_{2}(e^{i\omega}) $ ，然后利用傅里叶变换性质。]

(b) $ x_{3}[n] $的傅里叶变换 $ X_{3}(e^{j\omega}) $如图P5.26(c)所示，对 $ x_{3}[n] $重做(a)。

![图像（物理页 314，第 1 幅）](../Figures/fig-p0314-01.jpg){#fig:p314-1}

**图 P5.25**

![图像（物理页 314，第 2 幅）](../Figures/fig-p0314-02.jpg){#fig:p314-2}

(c) 设

$$
\alpha=\frac{\displaystyle\sum_{n=-\infty}^{\infty}n x_{1}[n]}{\displaystyle\sum_{n=-\infty}^{\infty}x_{2}[n]}
$$

这个 $ \alpha $ 量是信号 $ x_{1}[n] $ 的重心，通常称为 $ x_{1}[n] $ 的延迟时间。求 $ \alpha $ (做该题勿需首先明确地求出 $ x_{1}[n] $)。

**(a)**

(d) 考虑信号

$ x_{4}[n]=x_{1}[n]*h[n] $

其中

$$
h\left[n\right]=\frac{\sin\left(\pi n/6\right)}{\pi n}
$$

概略画出 $ X_{4}(e^{i\omega}) $。

5.27 (a) 设 x[n] 有傅里叶变换为 $ X(e^{j\omega}) $，如图 P5.27 所示。对于下列每一 p[n]，概略画出

**(b)**

$$
w[n]=x[n]p[n]
$$

![图像（物理页 314，第 3 幅）](../Figures/fig-p0314-03.jpg){#fig:p314-3}

![图像（物理页 314，第 4 幅）](../Figures/fig-p0314-04.jpg){#fig:p314-4}

的傅里叶变换。

**(c)**

**图 P5.26**

(i) $ p[n]=\cos\pi n $ (ii) $ p[n]=\cos(\pi n/2) $

(iv)

$$
p[n]=\sum_{k=0}^{\infty}\delta[n-2k]
$$

$$
p[~n~]=\sum_{k=-\infty}^{\infty}\delta[~n-4k~]
$$

(b) 假设(a)中的信号 w[n]作为输入加到一个单位脉冲响应为

$$
h\left[n\right]=\frac{\sin\left(\pi n/2\right)}{\pi n}
$$

的 LTI 系统上去，求对应于(a)中所选 p[n] 的输出 y[n]。

![图像（物理页 315，第 1 幅）](../Figures/fig-p0315-01.jpg){#fig:p315-1}

**图 P5.27**

5.28 已知信号 $ x[n] $ 和 $ g[n] $ 分别有傅里叶变换 $ X(e^{j\omega}) $ 和 $ G(e^{j\omega}) $，另外， $ X(e^{j\omega}) $ 和 $ G(e^{j\omega}) $ 之间的关系如下：

$$
\frac{1}{2\pi}\int_{-\pi}^{+\infty}X(\mathrm{e}^{\mathrm{j}\theta})G(\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta=1+\mathrm{e}^{-\mathrm{j}\omega}
$$

(a) 若 $ x[n] = (-1)^n $，求 $ g[n] $，使其傅里叶变换 $ G(e^{j\omega}) $ 满足 (P5.28-1) 式。对于 $ g[n] $ 还存在其它可能的解吗？

(b) 若 $ x[n] = \left(\frac{1}{2}\right)^{n}[n] $，重做(a)。

5.29 (a) 考虑一离散时间 LTI 系统，其单位脉冲响应为

$$
h[n]=\left(\frac{1}{2}\right)^{n} u[n]
$$

利用傅里叶变换求在下列各输入信号下的响应：

(i)

$$
x[n]=(\frac{3}{4})^{n}u[n]
$$

$$
x[n]=(n+1)(\frac{1}{4})^{n}u[n]
$$

$$
x[n]=(-1)^{n}
$$

(b) 假设

$$
h\left[n\right]=\left[\left(\frac{1}{2}\right)^{n}\cos\left(\frac{\pi n}{2}\right)\right]u\left[n\right]
$$

利用傅里叶变换求在下列各输入信号下的响应：

(i) $ x[n] = \left(\frac{1}{2}\right)^n u[n] $ (ii) $ x[n] = \cos(\pi n/2) $

(c) 设 x[n] 和 h[n] 的傅里叶变换为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=3\mathrm{e}^{\mathrm{j}\omega}+1-\mathrm{e}^{-\mathrm{j}\omega}+2\mathrm{e}^{-\mathrm{j}3\omega}\qquad H(\mathrm{e}^{\mathrm{j}\omega})=-\mathrm{e}^{\mathrm{j}\omega}+2\mathrm{e}^{-\tilde{2}\mathrm{j}\omega}+\mathrm{e}^{\mathrm{j}4\omega}
$$

求 $ y[n] = x[n] * h[n] $

5.30 在第4章曾指出过，单位冲激响应为

$$
h\left(t\right)=\frac{W}{\pi}{\mathrm{s i n c}}\Big(\frac{W t}{\pi}\Big)=\frac{\sin W t}{\pi t}
$$

的连续时间 LTI 系统在 LTI 系统分析中起着很重要的作用。同样正确的是单位脉冲响应为

$$
h\left[n\right]=\frac{W}{\pi}{\mathrm{s i n c}}\bigg(\frac{W n}{\pi}\bigg)=\frac{\sin W n}{\pi n}
$$

的离散时间 LTI 系统在 LTI 系统分析中也起着重要的作用。

(a) 求并画出单位脉冲响应为 $ h[n] $ 的系统的频率响应。

(b) 考虑信号

$$
x[n]=\sin\left(\frac{\pi n}{8}\right)-2\cos\left(\frac{\pi n}{4}\right)
$$

假定该信号是具有下列单位脉冲响应的 LTI 系统的输入，求每种情况的输出。

(i)

$$
h\left[n\right]=\frac{\sin\left(\pi n/6\right)}{\pi n}
$$

(ii)

(iii) $ h[n] = \frac{\sin(\pi n/6)\sin(\pi n/3)}{\pi^2 n^2} $

$$
h\left[n\right]=\frac{\sin\left(\pi n/6\right)}{\pi n}+\frac{\sin\left(\pi n/2\right)}{\pi n}
$$

$$
h\left[n\right]=\frac{\sin\left(\pi n/6\right)\sin\left(\pi n/3\right)}{\pi n}
$$

(c) 考虑单位脉冲响应为

$$
h[n]=\frac{\sin(\pi n/3)}{\pi n}
$$

的 LTI 系统，求对下列各输入信号下的输出：

(i) $ x[n]= $ 图 P5.30 的方波

$$
x[n]=\sum_{k=-\infty}^{\infty}\delta[n-8k]
$$

(iii) $ x[n] = (-1)^n $ 乘以图 P5.30 的方波

$$
x[n]=\delta[n+1]+\delta[n-1]
$$

![图像（物理页 316，第 1 幅）](../Figures/fig-p0316-01.jpg){#fig:p316-1}

**图 P5.30**

5.31 有一单位脉冲响应为 $ h[n] $，频率响应为 $ H(e^{j\omega}) $ 的 LTI 系统，当 $ -\pi \leqslant \omega_{0} \leqslant \pi $ 时具有如下特性 $ \cos\omega_{0}n \rightarrow \omega_{0}\cos\omega_{0}n $

(a) 求 $ H(e^{jw}) $ (b) 求 $ h[n] $

5.32 设 $ h_{1}[n] $ 和 $ h_{2}[n] $ 是因果 LTI 系统的单位脉冲响应，相应的频率响应是 $ H_{1}(e^{j\omega}) $ 和 $ H_{2}(e^{j\omega}) $，在这些条件下，下面的式子一般来说是对还是不对？陈述理由。

$$
\left[\frac{1}{2\pi}\int_{-\pi}^{\pi}H_{1}(\mathrm{e}^{\mathrm{j}\omega})\mathrm{d}\omega\right]\left[\frac{1}{2\pi}\int_{-\pi}^{\pi}H_{2}(\mathrm{e}^{\mathrm{j}\omega})\mathrm{d}\omega\right]=\frac{1}{2\pi}\int_{-\pi}^{\pi}H_{1}(\mathrm{e}^{\mathrm{j}\omega})H_{2}(\mathrm{e}^{\mathrm{j}\omega})\mathrm{d}\omega
$$

5.33 考虑一因果 LTI 系统，其差分方程为

$$
y[n]+\frac{1}{2}y[n-1]=x[n]
$$

(a) 求该系统的频率响应 $ H(e^{j\omega}) $

(b) 在下列输入时求系统响应：

(i) $ x[n] = \left(\frac{1}{2}\right)^n u[n] $ (ii) $ x[n] = \left(-\frac{1}{2}\right)^n u[n] $

(iii) $ x[n] = \delta[n] + \frac{1}{2}\delta[n-1] $ (iv) $ x[n] = \delta[n] - \frac{1}{2}\delta[n-1] $

(c) 在输入具有下列傅里叶变换时，求系统响应：

(ii) $X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}{1+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}$ (ii) $X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}{1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega}}$ (iii) $X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{(1-\frac{1}{4}\mathrm{e}^{-\mathrm{j}\omega})(1+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega})}$ (iv) $X(\mathrm{e}^{\mathrm{j}\omega})=1+2\mathrm{e}^{-\mathrm{j}\omega}$

5.34 考虑一个由两个 LTI 系统级联组成的系统，这两个系统的频率响应为

$$
H_{1}(\mathrm{e}^{\mathrm{j}\omega})=\frac{2-\mathrm{e}^{-\mathrm{j}\omega}}{1+\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}}\quad 和 \quad H_{2}(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{1-\frac{1}{2}\mathrm{e}^{-\mathrm{j}\omega}+\frac{1}{4}\mathrm{e}^{-\mathrm{j}2\omega}}
$$

(a) 求描述整个系统的差分方程。

(b) 求整个系统的单位脉冲响应。

### 5.35 一因果 LTI 系统由如下差分方程所描述： {#sec:5-35}

$$
y[n]-a y[n-1]=b x[n]+x[n-1]
$$

其中 a 为实数，且 $ |a| < 1 $。

(a) 找一个 b 值，使该系统的频率响应满足

$$
|H(e^{j\omega})|=1,
$$

值的输入 $ e^{j\omega t} $ 都不衰减，所以这类系统称为全通系统。利用该 b 值解余下的问题。

$$
\omega
$$

(b) 粗略画出当 $ a=1/2 $ 时 $ \leq H(e^{j\omega}), 0 \leq \omega \leq \pi_{0} $

(c) 粗略画出当 $ a = -1/2 $ 时 $ \leqslant H(e^{j\omega}) $, $ 0 \leqslant \omega \leqslant \pi_{0} $

(d) 当 $ a = -\frac{1}{2} $，系统的输入 $ x[n] $ 为

$$
x[n]=\left(\frac{1}{2}\right)^{n} u[n]
$$

求出并画出该系统的输出。由这个例子可见，一个非线性相移对信号造成的影响是明显不同于一个线性相移所引起的信号的时移的。

5.36 (a) 设 $ h[n] $ 和 $ g[n] $ 是两个互逆的离散时间 LTI 系统的单位脉冲响应，并且都是稳定的。问这两个系统频率响应之间是什么关系？

(b) 考虑由下列各差分方程描述的因果 LTI 系统，在每一种情况下，求逆系统的单位脉冲响应和表征该逆系统的差分方程。

(i)

$$
y[n]=x[n]-\frac{1}{4}x[n-1]
$$

(ii)

$$
y[n]+\frac{1}{2}y[n-1]=x[n]
$$

(iii)

$$
y[n]+\frac{1}{2}y[n-1]=x[n]-\frac{1}{4}x[n-1]
$$

$$
\left(\mathrm{iv}\right)y[n]+\frac{5}{4}y[n-1]-\frac{1}{8}y[n-2]=x[n]-\frac{1}{4}x[n-1]-\frac{1}{8}x[n-2]
$$

(v)

$$
y[n]+\frac{5}{4}y[n-1]-\frac{1}{8}y[n-2]=x[n]-\frac{1}{2}x[n-1]
$$

$$
\left(\mathrm{vi}\right)\ y[n]+\frac{5}{4}y[n-1]-\frac{1}{8}y[n-2]=x[n]
$$

(c) 考虑由下列差分方程所描述的因果离散时间 LTI 系统

$$
y[n]+y[n-1]+\frac{1}{4}y[n-2]=x[n-1]-\frac{1}{2}x[n-2]
$$

该系统的逆系统是什么？证明：逆系统是非因果的。试找出另一个因果 LTI 系统，它是由 (P5.36-1) 式描述的系统的“逆再加延时”，也即找一个因果 LTI 系统，使得图 P5.36 中的输出 w[n] 等于 $ x[n-1] $。

![图像（物理页 317，第 1 幅）](../Figures/fig-p0317-01.jpg){#fig:p317-1}

**图 P5.36**

**深入题**

5.37 设 $ X(e^{j\omega}) $ 是 x[n] 的傅里叶变换。利用 $ X(e^{j\omega}) $ 导出下列信号傅里叶变换表示式（没有假设 x[n] 是实序列）。

(a) $ \mathcal{R}\{x[n]\} $ (b) $ x^{*}[-n] $ (c) $ \mathcal{C}_{s}\{x[n]\} $

5.38 设 $ X(c^{jw}) $ 是一实信号 x[n] 的傅里叶变换，证明：x[n] 可以写成

$$
x[n]=\int_{0}^{\pi}\{B(\omega)\mathrm{c o s}\omega+C(\omega)\mathrm{s i n}\omega\}\mathrm{d}\omega
$$

（找出利用 $ X(e^{j\omega}) $ 来表示 $ B(\omega) $ 和 $ C(\omega) $ 的表示式）。

5.39 导出卷积性质

$$
x[n]*h[n]\xrightarrow{\mathcal{T}}X(\mathrm{e}^{\mathrm{j}\omega})H(\mathrm{e}^{\mathrm{j}\omega})
$$

5.40 x[n] 和 h[n] 是两个信号，并令 $ y[n] = x[n] \times h[n] $。试对 y[0] 写出两个表示式：一个利用 x[n] 和 h[n]（直接用卷积和）；另一个用 $ X(e^{j\omega}) $ 和 $ H(e^{j\omega}) $（用傅里叶变换的卷积性质）。然后，选择一个恰当的 h[n]，利用这两个表示式导出帕斯瓦尔定理，即

$$
\sum_{n=-\infty}^{+\infty}1\ x[n]1^{2}=\frac{1}{2\pi}\int_{-\pi}^{\pi}1\ X(e^{j\omega})1^{2}d\omega
$$

用类似的方式，导出下面帕斯瓦尔定理的一般形式：

$$
\sum_{n\quad\infty}^{+\infty}x\left[n\right]x^{*}\left[n\right]\simeq\frac{1}{2\pi}\int_{-\pi}^{\pi}X\left(\mathrm{e}^{\mathrm{j}\omega}\right)Z^{*}\left(\mathrm{e}^{\mathrm{j}\omega}\right)\mathrm{d}\omega
$$

5.41 令 $ \tilde{x}[n] $ 是一个周期为 N 的周期信号，另一有限长信号 x[n] 通过下式与 $ \tilde{x}[n] $ 关联：

$$
x[n]=\left|\begin{aligned}&\tilde{x}[n],&\quad n_{0}\leqslant n\leqslant n_{0}+N-1\\&0,&\quad 其余 n\end{aligned}\right.
$$

式子 $ n_{0} $ 为某整数。也就是说， $ x[n] $ 等于一个周期上的 $ \tilde{x}[n] $，而在其余地方均为零。

(a) 若 $ \tilde{x}[n] $ 的傅里叶级数系数为 $ a_{k} $， $ x[n] $ 的傅里叶变换为 $ X(e^{j\omega}) $，证明：

$$
u_{k}=\frac{1}{N}(\mathrm{e}^{j2\pi k/N})
$$

且与 $ n_{0} $ 的值无关。

(b) 考虑下面两个信号：

$$
x[n]=u[n]-u[n-5]\qquad\tilde{x}[n]=\sum_{k=-\infty}^{\infty}x[n-k N]
$$

这里 N 是一个正整数。令 $ a_{k} $ 记为 $ \tilde{x}[n] $ 的傅里叶系数， $ X(\mathrm{e}^{\mathrm{j}\omega}) $ 记为 $ x[n] $ 的傅里叶变换，

(i) 求 $ X(e^{\omega}) $ 的闭式表示式。

(ii) 利用(i)的结果，求傅里叶系数 $ a_{k} $ 的表示式。

5.42 本题将导出作为相乘性质的一种特殊情况的离散时间傅里叶变换的频移性质。令 x[n] 是任意离散时间信号，其傅里叶变换为 $ X(e^{i\omega}) $，并令

$$
g_{,}n]=e^{\mathrm{j}\omega_{0}n}x[n]
$$

(a) 求出并画出下面信号的傅里叶变换：

$$
p[n]=e^{j\omega_{0}n}
$$

$$
g[n]=p[n]x[n]
$$

$$
G(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{2\pi}\int_{<2\pi>}X(\mathrm{e}^{\mathrm{j}\theta})P((\mathrm{e}^{\mathrm{j}(\omega-\theta)})\mathrm{d}\theta
$$

求出这个积分以证明

$$
G(\mathrm{e}^{\mathrm{j}\omega})=X(\mathrm{e}^{\mathrm{j}(\omega-\omega_{0})})
$$

5.43 令 x[n] 的傅里叶变换为 $ X(e^{j\omega}) $，并令

$$
g[n]=x[2n]
$$

它的傅里叶变换是 $ G(e^{j\omega}) $。在本题中要导出 $ G(e^{j\omega}) $ 和 $ X(e^{j\omega}) $ 之间的关系。

(a) 设

$$
v[n]=\frac{(\mathrm{e}^{-\mathrm{j}\kappa n}x[n])+x[n]}{2}
$$

试用 $ X(e^{j\omega}) $ 表示 v[n] 的傅里叶变换 $ V(e^{j\omega}) $。

(b) 注意到，当 n 为奇数时， $ v[n]=0 $，证明 $ v[2n] $ 的傅里叶变换等于 $ V(e^{\frac{\omega}{2}}) $。

(c) 证明

$$
x[2n]=v[2n]
$$

于是就有

$$
G(\mathrm{e}^{\mathrm{j}\omega})=~V(\mathrm{e}^{\mathrm{j}\omega/2})
$$

现在利用(a)的结果，用 $ X(e^{jw}) $来表示 $ G(e^{jw}) $。

### 5.44 （a）令 {#sec:5-44}

$$
x_{1}[n]=\cos\left(\frac{\pi n}{3}\right)+\sin\left(\frac{\pi n}{2}\right)
$$

是一个信号， $ x_{1}[n] $ 的傅里叶变换记作 $ X_{1}(\mathrm{e}^{\mathrm{j}\omega}) $，画出 $ x_{1}[n] $ 和具有下列傅里叶变换的信号：

$$
\mathrm{(i)}X_{2}(\mathrm{e}^{\mathrm{j}\omega})=X_{1}(\mathrm{e}^{\mathrm{j}\omega})\mathrm{e}^{\mathrm{j}\omega},|\omega<\pi
$$

(ii) $ X_3(e^{j\omega}) = X_1(e^{j\omega}) e^{-j\beta\omega/2}, |\omega| < \pi $

(b) 令

$$
w(t)=\cos\Bigl(\frac{\pi t}{3T}\Bigr)+\sin\Bigl(\frac{\pi t}{2T}\Bigr)
$$

是一个连续时间信号。可以注意到， $ x_{1}[n] $ 可以看作是 $ w(t) $ 的等间隔采样的序列，即

$$
x_{1}[n]=w(n T)
$$

证明

$$
x_{2}[n]=w(nT-\alpha)\quad 和 \quad x_{3}[n]=w(nT-\beta)
$$

并给出 $ \alpha $ 和 $ \beta $ 的值。由此可以得出， $ x_{2}[n] $ 和 $ x_{3}[n] $ 也都是 $ w(t) $ 的等间隔样本序列。

5.45 考虑一离散时间信号 x[n]，其傅里叶变换如图 P5.45 所示。试画出下面连续时间信号，并予以标注：

(a)

$$
x_{1}(t)=\sum_{n=-\infty}^{\infty}x[n]\mathrm{e}^{\mathrm{j}(2\pi/10)n}
$$

(b)

$$
x_{2}(t)\;=\;\sum_{n=-\infty}^{\infty}x\big[-~n\big]\mathrm{e}^{\mathrm{j}(2\pi/10)n t}
$$

(c)

$$
x_{3}(t)=\;\sum_{n=-\infty}^{\infty}\mathcal{O d}\big\{x[n]\big\}e^{j(2\pi/8)n t}
$$

(d)

$$
{~)}x_{4}(t)\;=\;\sum_{n=-\infty}^{\infty}\mathcal{R}_{\mathfrak{e}}\big\vert x[n]\big\vert\mathrm{e}^{\mathrm{j}\left(2\pi/6\right)n t}
$$

![图像（物理页 319，第 1 幅）](../Figures/fig-p0319-01.jpg){#fig:p319-1}

![图像（物理页 319，第 2 幅）](../Figures/fig-p0319-02.jpg){#fig:p319-2}

**图 P5.45**

5.46 在例5.1中已证明了，对 $ \left|\alpha\right|<1 $有

$$
a^{n}u\left[n\right]\xrightarrow{\bar{x}}\frac{1}{1-a\mathrm{e}^{-\mathrm{j}\omega}}
$$

(a) 利用傅里叶变换性质，证明

$$
(n+1)\alpha^{n}u[n]{\overset{,}{\leftrightarrow}}\frac{1}{(1-\alpha\mathrm{e}^{-\mathrm{j}\omega})^{2}}
$$

(b) 用归纳法证明

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\frac{1}{(1-\alpha\mathrm{e}^{-\mathrm{j}\omega})^{r}}
$$

的傅里叶反变换是

$$
x[n]=\frac{(n+r-1)!}{n!(r-1)!}\alpha^{n} u[n]
$$

5.47 判定下列说法是对还是错，并陈述理由。下列每一条陈述中， $ x[n] $ 与 $ X(e^{j\omega}) $ 为一对傅里叶变换：

(a) 若 $ X(e^{\mathrm{j}\omega}) = X(e^{\mathrm{j}(\omega-1)}) $，则 $ x[n] = 0, |n| > 0 $

(b) 若 $ X(\mathrm{e}^{\mathrm{j}\omega}) = X(\mathrm{e}^{\mathrm{j}(\omega - \pi)}) $，则 $ x[n] = 0, |n| > 0 $

(c) 若 $ X(e^{j\omega}) = X(e^{j\omega/2}) $，则 $ x[n] = 0, |n| > 0 $

(d) 若 $ X(e^{j\omega}) = X(e^{j2\omega}) $，则 $ x[n] = 0, |n| > 0 $

5.48 已知一离散时间 LTI 的因果系统，其输入为 x[n]，输出为 y[n]。该系统由下面一对差分方程所表征：

$$
y[n]+\frac{1}{4}y[n-1]+w[n]+\frac{1}{2}w[n-1]=\frac{2}{3}x[n]
$$

$$
y[n]-\frac{5}{4}y[n-1]+2w[n]-2w[n-1]=-\frac{5}{3}x[n]
$$

其中 $ w[n] $ 是一个中间信号。

(a) 求该系统的频率响应和单位脉冲响应。

(b) 对该系统找出单一的关联 x[n] 和 y[n] 的差分方程。

5.49 (a) 有一离散时间系统，其输入为 x[n]，输出为 y[n]。它们的傅里叶变换由下式所关联：

$$
\mathrm{Y}(\mathrm{e}^{\mathrm{j}\omega})=2\mathrm{X}(\mathrm{e}^{\mathrm{j}\omega})+\mathrm{e}^{-\mathrm{j}\omega}\mathrm{X}(\mathrm{e}^{\mathrm{j}\omega})-\frac{\mathrm{d}\mathrm{X}(\mathrm{e}^{\mathrm{j}\omega})}{\mathrm{d}\omega}
$$

(i) 该系统是线性的吗？陈述理由。

(ii) 该系统是时不变的吗？陈述理由。

(iii) 若 $ x[n] = \delta[n] $，问 $ y[n] $ 是什么？

(b) 考虑一离散时间系统，其输出的傅里叶变换 $ Y(e^{j\omega}) $ 与输入的变换 $ X(e^{j\omega}) $ 关系如下：

$$
Y(\mathrm{e}^{\mathrm{j}\omega})=\int_{\omega-\pi/4}^{\omega+\pi/4}X(\mathrm{e}^{\mathrm{j}\omega})\mathrm{d}\omega
$$

找出用 x[n] 来表示 y[n] 的表示式。

5.50 (a) 假设想要设计一个离散时间 LTI 系统具有如下性质：若输入是

$$
x[n]=\left(\frac{1}{2}\right)^{n}u[n]-\frac{1}{4}\left(\frac{1}{2}\right)^{n-1}u[n-1]
$$

那么，输出就是

$$
y[n]=\left(\frac{1}{3}\right)^{n} u[n]
$$

(i) 求具有上述性质的离散时间 LTI 系统的单位脉冲响应和频率响应。

(ii) 求表征该系统的差分方程。

(b) 假定有一系统，它对输入 $ (n+2)(1/2)^n u(n) $ 的响应是 $ (1/4)^n u[n] $。问：若该系统的输出是 $ \delta[n] - (-1/2)^n u[n] $，输入该是什么？

5.51 (a) 考虑一离散时间系统，其单位脉冲响应为

$$
h[n]\left(\frac{1}{2}\right)^{n} u[n]+\frac{1}{2}\left(\frac{1}{4}\right)^{n} u[n]
$$

求一个关联该系统输入和输出的线性常系数差分方程。

(b) 图 P5.51 示出一个因果 LTI 系统的方框图实现：

(i) 求关联该系统 x[n] 和 y[n] 的差分方程。

(ii) 该系统的频率响应是什么?

(ii) 求该系统的单位脉冲响应。

![图像（物理页 321，第 1 幅）](../Figures/fig-p0321-01.jpg){#fig:p321-1}

5.52 (a) 设 $ h[n] $ 是一个实的，因果离散时间 LTI 系统，证明该系统可由它的频率响应的实部完全表征。

[提示：证明 $ h[n] $ 如何由 $ \mathcal{E}v\{h[n]\} $ 恢复， $ \mathcal{E}v\{h[n]\} $ 的傅里叶变换是什么？]

这就是与习题4.47中讨论的连续时间因果LTI系统的实部自满性质在离散时间下相对应的关系。

(b) 设 $ h[n] $ 为实且因果，若

$$
\mathcal{R}_{w}\{H(\mathrm{e}^{\mathrm{j}\omega})\|=1+\alpha\cos2\omega\quad(\alpha 为实数 )
$$

求 $ h[n] $ 和 $ H(e^{j\omega}) $

(c) 证明： $ h[n] $ 完全可由 $ \mathcal{I}_{m}|H(e^{j\omega})| $ 和 $ h[0] $ 恢复。

(d) 找出两个实的因果 LT1 系统，其频率响应的虚部都等于 $ \sin\omega $。

**扩充题**

5.53 在信号与系统的分析与综合中，离散时间方法应用的急剧增加，其原因之一就是由于对离散时间序列实现傅里叶分析的高效算法的出现。这些方法的核心是一种与离散时间傅里叶分析关系紧密，而又非常适合于应用数字计算机或以数字硬件实现的技术，称之为有限长序列的离散傅里叶变换(DFT)。

设 x[n] 是一有限长信号，即存在某一整数 $ N_{1} $，在 $ 0 \leqslant n \leqslant N_{1} - 1 $ 以外，有

$$
x[n]=0
$$

另外，令 x[n] 的傅里叶变换是 $ X(e^{j\omega}) $。现在可以构成一个周期信号 $ \tilde{x}[n] $， $ \tilde{x}[n] $ 在一个周期内等于 x[n]。也即，令 $ N \geqslant N_{1} $ 是一个已知的整数，并令 $ \tilde{x}[n] $ 的周期为 N，使之有

$$
\tilde{x}\left[n\right]=x\left[n\right],0\leqslant n\leqslant N-1
$$

$ \tilde{x}[n] $的傅里叶级数系数为

$$
a_{k}=\frac{1}{N}\sum_{(N)}\bar{x}\left[n\right]\mathrm{e}^{-\mathrm{j}k\left(2\pi/N\right)n}
$$

选取求和区间，以便在该区间内有 $ \hat{x}[n]=x[n] $，于是可得

$$
a_{k}=\frac{1}{N}\sum_{n=0}^{N-1}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n}
$$

由(P5.53-1)式所定义的系数就构成了 x[n] 的 DFT。x[n] 的 DFT 通常记作 $ \widetilde{X}[k] $。并定义为

$$
\widetilde{X}[k]=a_{k}=\frac{1}{N}\sum_{n=0}^{N-1}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n},\qquad k=0,1,\cdots,N-1
$$

DFT 的重要性来自于几个原因。第一，原先的有限长信号可以从它的 DFT 恢复，这就是

$$
x^{\lceil n\rceil}=\sum_{k=0}^{N-1}\widetilde{X}[k]e^{j k(2\pi/N)n},\quad n=0,1,\cdots,N-1
$$

因此，有限长信号既可以看成是由所给的有限个非零值所表征，也能看成是由它的有限个 DFT 值 $ \tilde{X}[k] $ 来确定。DFT 的第二个重要特点是对于它的计算有一个称之为快速傅里叶变换 (FFT) 的极快的算法 (见习题 5.54 对这一极为重要方法的介绍)。同时，由于它与离散时间傅里叶级数和变换之间的密切关系，DFT 本身就有一些傅里叶分析的重要特性。

![图像（物理页 322，第 1 幅）](../Figures/fig-p0322-01.jpg){#fig:p322-1}

**图 P5.53**

(a) 假设 $ N \geqslant N_{1} $，证明

$$
\widetilde{X}[k]=\frac{1}{N}X(e^{j(2\pi k/N)})
$$

式中 $ X[k] $ 是 x[n] 的 DFT。也就是说，DFT 就相应于 $ X(e^{j\omega}) $ 每隔 $ 2\pi/N $ 所取的样本值。(P5.53-3) 可以导致结论： $ x[n] $ 能唯一地由 $ X(e^{j\omega}) $ 的这些样本值来表示。

(b) 现在考虑每隔 $ 2\pi/M $, $ M < N_{1} $, 所取的 $ X(e^{\omega}) $ 的样本值。取得这些样本值所对应的序列就不仅是一个长度为 $ N_{1} $ 的序列。为了说明这一点，现考虑两个信号 $ x_{1}[n] $ 和 $ x_{2}[n] $，如图 P5.53 所示，证明：若取 M = 4，则对所有的 k 值有

$$
X_{1}(\mathrm{e}^{(j2\pi k/4)})=X_{2}(\mathrm{e}^{j(2\pi k/4)})
$$

5.54 正如在习题 5.53 所指出的，有许多实际上很重要的问题，都希望计算离散时间信号的 DFT。通常，这些信号的持续期很长，在这种情况下，使用高效的算法是非常重要的。使用计算机化的技术分析信号显著增长的原因之一就是出现了一种高效算法，这就是用来计算有限长序列 DFT 的所谓 FFT 算法。本题将讨论 FFT 的基本原理。

设 $ x[n] $ 是一个在区间 $ 0 \leqslant n \leqslant N_{1}-1 $ 以外为零的信号，对于 $ N \geqslant N_{1} $， $ x[n] $ 的 N 点 DFT 为

$$
\widetilde{X}[k]=\frac{1}{N}\sum_{k=0}^{N-1}x[n]\mathrm{e}^{-\mathrm{j}k(2\pi/N)n},\quad k=0,1,\cdots,N-1
$$

为了方便，将(P5.54-1)式改写为

$$
\widetilde{X}[k]=\frac{1}{N}\sum_{k=0}^{N-1}x[n]W_{N}^{nk}
$$

式中

$$
\mathbf{W}_{N}=\mathrm{e}^{-\mathrm{j}2\pi/N}
$$

(a) 计算 $ \dot{X}[k] $ 的一个方法是直接计算 (P5.54-2) 式。对这种计算的复杂程度的一种有用度量是所需复数乘法的总数。证明，对 $ k=0,1,\cdots,N-1 $，直接计算 (P5.54-2) 式所需要的复数乘法次数是 $ N^{2} $。假定 $ x \in n $ 是复数，且所需要的 $ W_{N}^{k} $ 的值已经都预先计算出来，并存放在一张表格中。为简单起见，不计如下情况：对于某些 n 和 k 的值， $ W_{N}^{k} $ 等于 $ \pm1 $ 或 $ \pm j $，因而严格说来并不需要全部做复数乘法。

(b) 假设 N 是偶数。令 $ f[n] = x[2n] $ 表示 $ x[n] $ 的偶数下标样本，令 $ g[n] = x[2n + 1] $ 表示 $ x[n] $ 的

奇数下标样本。

(i) 证明： $ f[n] $ 和 $ g[n] $ 在区间 $ 0 \leqslant n \leqslant (N/2) - 1 $ 以外是零。

(ii) 证明： $ x[n] $ 的 N 点 DFT $ X[k] $ 可以表示为

$$
\begin{aligned}{\widetilde{X}[k]={}}&{{}\frac{1}{N}\sum_{n=0}^{(N/2)-1}f[n]W_{N/2}^{n}+\frac{1}{N}W_{N}^{k}\sum_{n=0}^{(N/2)-1}g[n]W_{N/2}^{n}}\\ {={}}&{{}\frac{1}{2}\widetilde{F}[k]+\frac{1}{2}W_{N}^{k}\widetilde{G}[k],~k=0,1,\cdots,N-1}\\ \end{aligned}
$$

式中

$$
\begin{aligned}{\widetilde{F}[k]}&{{}=\frac{2}{N}\sum_{n=0}^{(N/2)-1}f[n]W_{N/2}^{n k}}\\ {\widetilde{G}[k]}&{{}=\frac{2}{N}\sum_{n=0}^{(N/2)-1}g[n]W_{N/2}^{n k}}\\ \end{aligned}
$$

(iii) 证明：对所有 k，有

$$
\begin{aligned}{\widetilde{F}\Big[k+\frac{N}{2}\Big]}&{{}=\widetilde{F}\big[k\big]}\\ {\widetilde{G}\Big[k+\frac{N}{2}\Big]}&{{}=\widetilde{G}\big[k\big]}\\ \end{aligned}
$$

注意： $ \widetilde{F}[k], k=0,1,\cdots,(N/2)-1 $，和 $ \widetilde{G}[k], k=0,1,\cdots,(N/2)-1 $ 分别是 $ f[n] $ 和 $ g[n] $ 的N/2点DFT。因此，(P5.54-3)式表明， $ x[n] $ 的长度为N点DFT 可以用两个长度为N/2的DFT来计算。

(iv) 当根据(P5.54-3)式，通过先计算 $ F[k] $ 和 $ G[k] $ 来计算 $ X[k] $， $ k=0,1,\cdots,N-1 $ 时，确定所需要的复数乘法次数。[有关做乘法时的假定与(a)相同，且不计入(P5.54-3)式中乘1/2量的运算。]

(c) 若像 N 一样，N/2 还是偶数，则 $ f[n] $ 和 $ g[n] $ 都可以被分解为偶数下标和奇数下标的样本序列。因此，它们的 DFT 可以利用与 (P5.54-3) 式中相同的步骤来计算。进而，若 N 是 2 的整数幂，就可以继续重复这一过程，从而有效地节省计算时间。当 N = 32, 256, 1024 和 4096 时，用这个过程来做，大约各需要多少次数乘法？试将此方法与 (a) 中的直接计算法作一比较。

5.55 本题将介绍“加窗”的概念，它无论在 LTI 系统的设计，还是在信号的频谱分析中都具有非常大的重要性。“加窗”就是把信号 x[n] 乘上一个有限长的窗口信号 w[n] 的一种运算，也就是

$$
\phi[n]=x[n]w[n]
$$

注意， $ p[n] $也是有限长的。

在频谱分析中，加密的重要性来自于：在大量应用场合，人们总是希望计算被测信号的傅里叶变换。由于在实际中，我们只能在有限时间区间（即时窗）上测得信号 x[n]，因而对频谱分析来说，实际可利用的信号是

$$
p\left[n\right]=\left\{\begin{aligned}&x[n],&-M\leqslant n\leqslant M\\ &0,& 其余 n\end{aligned}\right.
$$

其中 $ -M \leqslant n \leqslant M $就是时窗。于是

$$
p[n]=x[n]w[n]
$$

这里 $ w[n] $ 是矩形窗，即

$$
w[n]=\left\{\begin{aligned}&1,-M\leqslant n\leqslant M\\ &0, 其余 n\end{aligned}\right.
$$

“加窗”在LTI系统设计中也起着重要的作用。具体地说，由于种种原因[例如FFT算法的潜在应用；见习题P5.54]，需要设计一个具有有限长脉冲响应的系统，以便达到某种要求的信号处理目的；也

就是说，往往从所需要的频率响应 $ H(e^{j\omega}) $ 开始，它的反变换 $ h[n] $ 是一个无限长（或至少是非常长）的单位脉冲响应，而要求构成一个有限长单位脉冲响应 $ g[n] $，使它的傅里叶变换 $ G(e^{j\omega}) $ 充分地逼近 $ H(e^{j\omega}) $。选择 $ g[n] $ 的一般方法是找一个窗函数 $ w[n] $，使 $ h[n]w[n] $ 的傅里叶变换满足所需要的 $ G(e^{j\omega}) $ 的指标要求。

很明显，将一个信号加密对所得到的频谱是会有影响的，本题将说明这种影响。

(a) 为了对加窗的效果加深理解，现用(P5.55-1)式所给的矩形窗对信号

$$
x[n]=\sum_{k=-\infty}^{\infty}\hat{o}[n-k]
$$

进行加窗。

(i) $ X(e^{j\omega}) $ 是什么？

（ii）当 M=1，概略画出 $ p[n]=x[n]w[n] $ 的变换。

(iii) 当 M=10，重做(ii)。

(b) 考虑一信号 x[n]，其傅里叶变换为

$$
X(\mathrm{e}^{\mathrm{j}\omega})=\left\{\begin{aligned}&1,\text{i}\omega<\pi/4\\ &0,\pi/4<\mathrm{i}\omega\leq\pi\end{aligned}\right.
$$

设 $ p[n]=x[n]w[n] $，这里 $ w[n] $ 是 $ (P5.55-1) $ 式的矩形窗。对 M=4,8 和 16，大致画出 $ P(e^{jw}) $。

(c) 应用矩形窗的一个问题是它在变换 $ P(e^{\omega}) $ 中引入了起伏（这一点是与吉伯斯现象直接有关的）。由于这个原因，又研究了其它各种窗口信号，这些窗口信号不是陡峭变化的，也就是说，它们从 0 到 1 的变化要比矩形窗的陡峭变化平缓得多。这样做是为了利用进一步平滑 $ X(e^{\omega}) $，从而增加一点失真作为代价来减小 $ P(e^{\omega}) $ 中的起伏。

为了说明上面这一点，考虑(b)中所描述的信号 $ x[n] $，并设 $ p[n] = x[n]w[n] $，这里 $ w[n] $ 是三角形窗或巴特利特(Bartlett)窗，即

$$
w[n]=\left\{\begin{aligned}&1-\frac{|n|}{M+1},&-M\leqslant n\leqslant M\\ &0,& 其余 n\end{aligned}\right.
$$

对于 M=4, 8 和 16, 大致画出 $ p[n]=x[n]w[n] $ 的傅里叶变换。

[提示：注意三角形信号可以作为矩形信号与它自身的卷积得到，这会导致 $ W(e^{w}) $ 一个方便的表达式。]

(d) 设 $ p[n] = x[n]w[n] $，这里 $ w[n] $ 是一个升余弦信号，称之为海宁(Hanning)窗，即

$$
w[n]=\left\{\begin{aligned}&\frac{1}{2}[1+\cos(\pi n/M)],&\quad&-M\leqslant n\leqslant M\\&0,&\quad& 其余 \ n\end{aligned}\right.
$$

对于 M=4, 8 和 16, 大致画出 $ P(e^{jw}) $

5.56 设 $ x[m, n] $ 是一个信号，它是两个独立的离散变量 m 和 n 的函数。和一维的情况，以及与在习题 4.53 中处理的连续时间情况相类似，可以定义 x[m, n] 的二维傅里叶变换为

$$
X(\mathrm{e}^{\mathrm{j}\omega_{1}},\mathrm{e}^{\mathrm{j}\omega_{2}})=\sum_{n=-\infty}^{\infty}\sum_{m=-\infty}^{\infty}x[m,n]\mathrm{e}^{-\mathrm{j}\left(\omega_{1}m+m_{2}n\right)}
$$

(a) 证明: (P5.56-1) 式可以按照两个逐次的一维傅里叶变换来计算，即先对 m 变换，而认为 n 是固定的；然后再对 n 变换。利用这一结果，确定用 $ X(e^{j\omega_1}, e^{j\omega_2}) $ 表示 x[m, n] 的表达式。

(b) 假设

$$
x[m,n]=a[m]b[n]
$$

其中 $ a[m] $ 和 $ b[n] $ 都是一个独立变量的函数。设 $ A(e^{j\omega}) $ 和 $ B(e^{j\omega}) $ 分别代表 $ a[m] $ 和 $ b[n] $ 的傅里叶变换，试用 $ A(e^{j\omega}) $ 和 $ B(e^{j\omega}) $ 来表示 $ X(e^{j\omega_1}, e^{j\omega_2}) $。

(c) 求下列信号的二维傅里叶变换：

(i) $ x[m, n] = \delta[m-1] \delta[n+4] $

(ii) $ x[m, n] = \left(\frac{1}{2}\right)^{n-m} u[n-2] u[-m] $

(iii) $ x[m, n] = \left(\frac{1}{2}\right)^n \cos(2\pi m/3) u[n] $

(iv) $ x[m, n] = \begin{cases} 1, & -2 < m < 2 \text{ 和 } -4 < n < 4 \\ 0, & \text{其它 } m \text{ 和 } n \end{cases} $

(v) $ x[m, n] = \left\{ \begin{aligned} 1, & -2 + n < m < 2 + n \text{ 和 } -4 < n < 4 \\ 0, & \text{ 其它 } m \text{ 和 } n \end{aligned} \right. $

(vi) $ x[m, n] = \sin\left(\frac{\pi n}{3} + \frac{2\pi m}{5}\right) $

(d) 已知信号 $ x[m, n] $ 的傅里叶变换为

$$
\mathrm{X}(\mathrm{e}^{\mathrm{j}\omega_{1}},\mathrm{e}^{\mathrm{j}\omega_{2}})=\left\{\begin{aligned}&1,0<|\omega_{1}|\leqslant\pi/4 和 0<|\omega_{2}|\leqslant\pi/2\\&\theta,\pi/4<|\omega_{1}|<\pi 或 \pi/2<\mathrm{`}\omega_{2}|<\pi\end{aligned}\right.
$$

求 $ x[m, n] $。

(e) 设 $ x[m, n] $ 和 $ h[m, n] $ 是两个信号，它们的二维傅里叶变换分别为 $ X(e^{j\omega_{1}}, e^{j\omega_{2}}) $ 和 $ H(e^{j\omega_{1}}, e^{j\omega_{2}}) $。

试用 $ X(e^{j\omega_{1}}, e^{j\omega_{2}}) $ 和 $ H(e^{j\omega i_{1}}, e^{j\omega_{2}}) $ 表示下列信号的傅里叶变换式：

$$
x[m,n]\mathrm{e}^{\mathrm{j}\omega_{1}m}\mathrm{e}^{\mathrm{j}\omega_{2}n}
$$

(ii) $ y[m, n] = \left\{ \begin{aligned} & x[k, r], & \text{若 } m = 2k, \ n = 3r \\ & 0, & \text{若 } m \text{ 不是 } 2 \text{ 的倍数}, \text{ 或 } n \text{ 不是 } 3 \text{ 的倍数} \end{aligned} \right. $

(iii) $ y[m, n] = x[m, n]h[m, n] $
