## 第9章 拉普拉斯变换 {#sec:9}

### 9.0 引 言 {#sec:9-0}

前面几章已经看到，傅里叶分析工具在研究涉及信号和LTI系统的很多问题中是极为有用的。这在很大程度上是由于相当广泛的一类信号都能用周期复指数信号的线性组合来表示，而复指数信号又是LTI系统的特征函数的缘故。连续时间傅里叶变换提供了将信号表示成形如 $ e^{x} $， $ s=j\omega $的复指数信号的线性组合；然而，由3.2节引入的特征函数性质及其它的很多结果对任意s值都是适用的，而并不是将它仅限于纯虚数的情况。这样的看法就导致了连续时间傅里叶变换的推广，称之为拉普拉斯变换，这就是本章要进行讨论的。下一章将建立对应的离散时间的推广，称之为z变换。

将会看到，拉普拉斯变换和z变换都有很多使傅里叶变换成为如此有用的那些性质。然而，这些变换不仅仅是对那些能用傅里叶变换进行分析的信号与系统提供了另一种分析工具和另一种分析的角度，而且在一些傅里叶变换不能应用的重要方面，它们也能够应用。例如：拉普拉斯变换和z变换能用于许多不稳定系统的分析，这样就在系统的稳定性或不稳定性的研究中起着重要的作用。这一事实再与拉普拉斯变换和z变换与傅里叶变换共有的代数性质组合在一起，就形成了一整套重要的系统分析工具，尤其是在第11章要讨论的反馈系统分析中更是如此。

### 9.1 拉普拉斯变换 {#sec:9-1}

在第3章已经知道，一个单位冲激响应为 $ h(t) $的线性时不变系统，对 $ e^{x} $复指数输入信号的响应 $ y(t) $是

$$
y(t)=H(s)\mathrm{e}^{s}
$$

这里

$$
H(s)=\int_{-\infty}^{\infty}h(t)\mathrm{e}^{-st}\mathrm{d}t
$$

若 s 为虚数（即 $ s = j\omega $），(9.2) 式的积分就对应于 $ h(t) $ 的傅里叶变换。对一般的复变量 s 来说，(9.2) 式就称为单位冲激响应 $ h(t) $ 的拉普拉斯变换。

一个信号 $ x(t) $ 的拉普拉斯变换定义如下 $ ^{①} $:

$$
X(s)\triangleq\int_{-\infty}^{+\infty}x(t)\mathrm{e}^{-st}\mathrm{d}t
$$

应该特别注意到，这是一个自变量为 s 的函数，而 s 是在 $ e^{-s} $ 中指数的复变量。复变量 s 一般可写成 $ s = \sigma + j\omega $，其中 $ \sigma $ 和 $ \omega $ 分别是它的实部和虚部。为方便起见，常将拉普拉斯变换表示为算子 $ x|x(t)| $ 形式，而把 $ x(t) $ 和 $ X(s) $ 间的变换关系记为

$$
x(t)\overset{T}{\leftrightarrow}X(s)
$$

当 $ s=j\omega $ 时，(9.3)式就变成

$$
X(\mathrm{j}\omega)=\int_{-\infty}^{+\infty}x(t)\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t
$$

这就是 $ x(t) $ 的傅里叶变换，即

$$
X(s)\mid_{s=\mathrm{j}\omega}=\mathcal{F}\{x(t)\}
$$

当复变量 s 不为纯虚数时，拉普拉斯变换与傅里叶变换也有一个直接的关系。为了看出这一点，将(9.3)式 $ X(s) $ 中的 s 表示成 $ s = \sigma + j\omega $，则有

$$
X(\sigma+\mathrm{j}\omega)=\int_{-\infty}^{+\infty}x(t)\mathrm{e}^{-(\sigma+\mathrm{j}\omega)t}\mathrm{d}t
$$

或者

$$
X(\sigma+\mathrm{j}\omega)=\int_{-\infty}^{+\infty}[x(t)\mathrm{e}^{-\sigma t}]\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t
$$

我们可以把(9.8)式的右边看作 $ x(t)e^{-\alpha t} $ 的傅里叶变换。这就是说， $ x(t) $ 的拉普拉斯变换可以看成是 $ x(t) $ 在乘以一个实指数信号以后的傅里叶变换。这个实指数 $ e^{-\alpha t} $ 在时间上可以是衰减的，或者是增长的，这决定于 $ \sigma $ 是正还是负。

为了说明拉普拉斯变换，以及它与傅里叶变换的关系，考虑下面的例子。

例 9.1 设信号 $ x(t)=\mathrm{e}^{-at}u(t) $，由例 4.1，它的傅里叶变换 $ X(j\omega) $ 在 a>0 时收敛，且为

$$
X(j\omega)=\int_{-\infty}^{+\infty}\mathrm{e}^{-at}u(t)\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t=\int_{0}^{\infty}\mathrm{e}^{-at}\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t=\frac{1}{\mathrm{j}\omega+a},~a>0
$$

根据(9.3)式，其拉普拉斯变换为

$$
X(s)=\int_{-\infty}^{\infty}\mathrm{e}^{-\omega t}u(t)\mathrm{e}^{-s t}\mathrm{d}t=\int_{0}^{\infty}\mathrm{e}^{-(s+a)t}\mathrm{d}t
$$

或者，用 $ s = \sigma + j\omega $

$$
X(\sigma+\mathrm{j}\omega)=\int_{0}^{\infty}\mathrm{e}^{-\left(\sigma+a\right)t}\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t
$$

将(9.11)式与(9.9)式相比较，可以看出(9.11)式就是 $ \mathrm{e}^{-(\sigma+a)t} u(t) $ 的傅里叶变换，于是有

$$
X(\sigma+\mathrm{j}\omega)=\frac{1}{(\sigma+a)+\mathrm{j}\omega},\mathrm{~}\sigma+a>0
$$

因为 $ s = \sigma + j\omega $ 和 $ \sigma = \mathcal{A}\{s\} $，又可等效为

$$
X(s)=\frac{1}{s+a},\;\mathcal{R}\{s\}>-a
$$

这就是

$$
\mathrm{e}^{-a t}u(t)\xrightarrow{t}\frac{1}{s+a},\quad\mathcal{R}_{\mathrm{e}}\vert_{s}\vert>-a
$$

例如，若 a=0, $ x(t) $ 就是单位阶跃函数，其拉普拉斯变换为 $ X(s)=1/s $, $ \mathcal{R}_{0}\{s\}>0 $。

从这个例子应该特别注意到，正如傅里叶变换不是对所有信号都收敛一样，拉普拉斯变472

换也可能对某些 $ \mathcal{R}\{s\} $值收敛，而对另一些 $ \mathcal{R}\{s\} $则不收敛。在(9.13)式中，该拉普拉斯变换仅对 $ \sigma=\mathcal{R}\{s\}>-a $收敛，如果a为正值，那么， $ X(s) $就能在 $ \sigma=0 $求值，而得到

$$
X(0+\mathrm{j}\omega)=\frac{1}{\mathrm{j}\omega+a}
$$

如(9.6)式所指出的，对于 $ \sigma=0 $，拉普拉斯变换就等于傅里叶变换，这只要将(9.9)式和(9.15)式比较一下就能看出。如果a是负的或为零，拉普拉斯变换仍然存在，但傅里叶变换却不存在。

例9.2 为了与例9.1相比较，现考虑第二个例子。信号 $ x(t) $为

$$
x(t)=-\mathrm{e}^{-at}u(-t)
$$

那么

$$
\begin{aligned}X(s)&=-\int_{-\infty}^{\infty}\mathrm{e}^{-at}\mathrm{e}^{-st}u(-t)\mathrm{d}t\\&=-\int_{-\infty}^{0}\mathrm{e}^{-(s+a)t}\mathrm{d}t\end{aligned}
$$

或者

$$
X(s)=\frac{1}{s+a}
$$

对这个例子，为保证收敛，则要求 $ \varnothing_{e}\mid_{s}+a\mid<0 $，或者 $ \varnothing_{e}\mid_{s}\mid<-a $，这就是说

$$
-\mathrm{e}^{-a t}u(-\mathrm{\boldmath~t~}){\overset{x}{\leftrightarrow}}\frac{1}{s+a},\quad\mathcal{R}\{s\}<-a
$$

比较一下(9.14)式和(9.19)式可见，对例9.1和例9.2中的两个信号，它们的拉普拉斯变换代数表示式都是一样的；然而，这个代数表示式能成立的s域却是大不相同的。这就说明，在给出一个信号的拉普拉斯变换时，代数表示式和该表示式能成立的变量s值的范围都应该给出。一般把使积分(9.3)式收敛的s值的范围称为拉普拉斯变换的收敛域，特简记作ROC。也就是说，ROC是由这样一些 $ s=\sigma+j\omega $组成的，对这些s来说， $ x(t)e^{-\alpha t} $的傅里叶变换收敛。随着我们深入讨论拉普拉斯变换的性质，关于ROC将有更多的话要说。

![图像（物理页 497，第 1 幅）](../Figures/fig-p0497-01.jpg){#fig:p497-1}

**图 9.1 (a) 例 9.1 的 ROC; (b) 例 9.2 的 ROC**

表示收敛域 ROC 的一个方便的办法是如图 9.1 所示。变量 s 是一个复数，在图 9.1 上展示出的复平面，一般就称为与这个复变量有关的 s 平面。沿水平轴是 $ \mathbb{R} \setminus \{s\} $ 轴，垂直轴是

$ I_{m}\{s\} $轴，水平轴和垂直轴有时分别称为 $ \sigma $ 轴和 $ j\omega $ 轴。图9.1(a)的阴影部分就是对应于例9.1的收敛域；而图9.1(b)的阴影部分指出了例9.2的收敛域。

例 9.3 本例考虑的信号是两个实指数信号的和，即

$$
x(t)=3\mathrm{e}^{-2t}u(t)-2\mathrm{e}^{-\tau}u(t)
$$

于是其拉普拉斯变换的代数表示式为

$$
\begin{aligned}X(s)&=\int_{-\infty}^{\infty}\left[3\mathrm{e}^{-2t}u(t)-2\mathrm{e}^{-t}u(t)\right]\mathrm{e}^{-s t}\mathrm{d}t\\&=3\int_{-\infty}^{\infty}\mathrm{e}^{-2t}\mathrm{e}^{-s t}u(t)\mathrm{d}t-2\int_{-\infty}^{\infty}\mathrm{e}^{-t}\mathrm{e}^{-s t}u(t)\mathrm{d}t\end{aligned}
$$

(9.21)式中的每个积分式都与(9.10)式的积分式具有相同的形式，这样就能利用例9.1的结果而得到

$$
X(_{s})=\frac{3}{s+2}-\frac{2}{s+1}
$$

为了确定它的 ROC，我们注意到，因为 $ x(t) $ 是两个实指数信号的和，而由(9.21)式可知， $ X(s) $ 是单独每一项的拉普拉斯变换之和。第一项是 $ 3e^{-2t}u(t) $ 的拉普拉斯变换，而第二项是 $ -2e^{-t}u(t) $ 的拉普拉斯变换。由例 9.1 知道

$$
\begin{aligned}{}&{{}\operatorname{e}^{-t}u(t){\leftrightarrow}\frac{1}{s+1},\quad\mathcal{R e}\{s\}|>-1}\\ {}&{{}\operatorname{e}^{-2t}u(t){\leftrightarrow}\frac{1}{s+2},\quad\mathcal{R e}\{s\}>-2}\\ \end{aligned}
$$

于是，使这两项拉普拉斯变换都收敛的那些 $ \mathcal{R}_n\mid s\mid $ 值的集合就是 $ \mathcal{R}_n\{s\mid> -1 $，这样把(9.22)式右边这两项合起来，就得到

$$
3\mathrm{e}^{-2t}u(t)-2\mathrm{e}^{-t}u(t){\stackrel{\mathcal{L}}{\leftrightarrow}}\frac{s-1}{s^{2}+3s+2},\quad\mathcal{R e}\{s\}>-1
$$

例 9.4 本例要考虑实指数和复指数之和的信号为

$$
x(t)=\mathrm{e}^{-2t}u(t)+\mathrm{e}^{-t}(\cos3t)u(t)
$$

利用欧拉关系，可写为

$$
x(t)=\bigg[\mathrm{e}^{-2t}+\frac{1}{2}\mathrm{e}^{-(1-3i)t}+\frac{1}{2}\mathrm{e}^{-(1+3i)t}\bigg]u(t)
$$

那么 $ x(t) $ 的拉普拉斯变换就能表示成

$$
\begin{aligned}{X(s)}&{{}=\int_{-\infty}^{\infty}\mathbf{e}^{-2t}u(t)\mathbf{e}^{-\varsigma}\mathrm{d}t}\\ {}&{{}+\frac{1}{2}\int_{-\infty}^{\infty}\mathbf{e}^{-(1-3j)t}u(t)\mathbf{e}^{-\varsigma}\mathrm{d}t}\\ {}&{{}+\frac{1}{2}\int_{-\infty}^{\infty}\mathbf{e}^{-(1+3j)t}u(t)\mathbf{e}^{-\varsigma}\mathrm{d}t}\\ \end{aligned}
$$

(9.25)式中的每一个积分都代表了在例9.1中所遇到过的拉普拉斯变换，即

$$
\mathrm{e}^{-2t}u\left(t\right)\xrightarrow{\mathcal{X}}\frac{1}{s+2},\;\mathcal{R e}\left\{s\right\}>-2
$$

$$
\mathrm{e}^{-(1-3j)t}u(t)\xrightarrow{x}\frac{1}{s+(1-3j)},\;\mathcal{R}_{*}\{s\}>-1
$$

$$
\mathrm{e}^{-(1+3\mathrm{j})\iota}u\left(t\right){\overset{\mathcal{F}}{\longleftrightarrow}}\frac{1}{s+\left(1+3\mathrm{j}\right)},\mathcal{R}_{\mathrm{e}}|s|>-1
$$

为了使这三个拉普拉斯变换都同时收敛，必须有 $ \mathcal{R}|s|>-1 $，因此， $ x(t) $ 的拉普拉斯变换为

$$
\frac{1}{s+2}+\frac{1}{2}\Big(\frac{1}{s+(1-3j)}\Big)+\frac{1}{2}\Big(\frac{1}{s+(1+3j)}\Big),\quad\mathcal{R e}\nmid s\mid>-1
$$

或者，合并为公共分母得

$$
\mathrm{e}^{-2t}u\left(t\right)+\mathrm{e}^{-2t}(\cos3t)u\left(t\right)\xrightarrow{u}\frac{2s^{2}+5s+12}{(s^{2}+2s+10)(s+2)},\quad\mathcal{R}_{n}|_{s}|>-1
$$

以上4个例子的每一个，其拉普拉斯变换式都是有理的，也即都是复变量s的两个多项式之比，具有如下形式：

$$
X(s)=\frac{N(s)}{D(s)}
$$

其中 $ N(s) $ 和 $ D(s) $ 分别是分子多项式和分母多项式。正如在例 9.3 和例 9.4 中所见到的，只要 $ x(t) $ 是实指数或复指数信号的线性组合， $ X(s) $ 就一定是有理的。并且，在 9.7 节将会看到，当 LTI 系统是用线性常系数微分方程表征时，也会见到有理的变换。除去一个常数因子外，在一个有理拉普拉斯变换式中，分子与分母多项式都能够用它们的根来表示，据此，在 s 平面内标出 $ N(s) $ 和 $ D(s) $ 根的位置，并指出收敛域 ROC 就提供了一种描述拉普拉斯变换的方便而形象的表示。例如，如果用“×”来表示 (9.23) 式中分母多项式每一个根的位置；用“○”来表示 (9.23) 式中分子多项式每一个根的位置，在图 9.2 (a) 中就展示了例 9.3 的拉普拉斯变换的 s 平面表示。图 9.2(b) 则是例 9.4 的拉普拉斯变换式分子和分母多项式的根所对应的图。每一个例子的收敛域都在相应的图上用阴影区给出。

对于有理拉普拉斯变换来说，因为在分子多项式的那些根上 $ X(s)=0 $，故称为 $ X(s) $的零点；而在分母多项式的那些根上， $ X(s) $变成无界，故称分母多项式的根为 $ X(s) $的极点。在有限s平面内， $ X(s) $的零点和极点，除了一个常数因子外可以完全表征 $ X(s) $的代数表示式。通

![图像（物理页 499，第 1 幅）](../Figures/fig-p0499-01.jpg){#fig:p499-1}

![图像（物理页 499，第 2 幅）](../Figures/fig-p0499-02.jpg){#fig:p499-2}

**图9.2 (a)和(b)分别为例9.3和例9.4的拉普拉斯变换的s平面表示。图中每一个×标出相应拉普拉斯变换的一个极点位置，也就是分母多项式一个根的位置。同理，每个○标出一个零点，即分子多项式一个根的位置。ROC用阴影区指出**

过在 s 平面内的极点和零点的 $ X(s) $ 的表示就称为 $ X(s) $ 的零极点图。然而，正如在例 9.1 和例 9.2 所看到的， $ X(s) $ 的代数表示式本身并不能确认该拉普拉斯变换的 ROC。这也就是说，除了一个常数因子外，一个有理拉普拉斯变换的完全表征是由该变换的零极图与它的 ROC

一起组成的(一般在s平面内，ROC用阴影区表示，如图9.1和图9.2所示)。

另外，虽然不一定都需要给出一个有理变换 $ X(s) $ 的代数表示式，但是有时为了指明 $ X(s) $ 在无限远点的极点或零点，有了代数表示式倒是较为方便的。这就是，如果分母多项式的阶次是高于分子多项式的阶次，那么 $ X(s) $ 将随 s 趋于无限大而变为零。相反，若分子多项式的阶次是高于分母多项式的阶次，那么 $ X(s) $ 将随 s 趋于无限大而变成无界。这样一种特性就可以把它们看作在无限远处的零点或极点。例如，在 (9.23) 式中的拉普拉斯变换其分母的阶为 2，而分子的阶仅为 1，所以在这个情况下， $ X(s) $ 在无限远点有一个零点。同样，在 (9.30) 式的拉普拉斯变换，其分子的阶为 2，而分母的阶是 3，在无限远点也有一个零点。一般来说，如果分母的阶次高出分子的阶次为 k 次，则 $ X(s) $ 一定在无限远点有 k 阶零点；同理，若分子的阶次超过分母的阶次为 k 次， $ X(s) $ 在无限远点一定有 k 阶极点。

**例 9.5 设信号 $ x(t) $ 为**

$$
x(t)=\delta(t)-\frac{4}{3}\mathrm{e}^{-t}u(t)+\frac{1}{3}\mathrm{e}^{2t}u(t)
$$

(9.32)式中右边第二和第三项的拉普拉斯变换都可由例9.1求出，而单位冲激函数的拉普拉斯变换可直接求出为

$$
\mathcal{L}\big|\delta(t)\big|=\int_{-\infty}^{+\infty}\delta\big(t\big)\mathrm{e}^{-s t}\mathrm{d}t=1
$$

该结果对任何 s 值都成立。这就是说， $ \mathcal{L}[\delta(t)] $ 的 ROC 是整个 s 平面。利用这个结果。再与(9.32)式其余两项一起就得出

$$
X(s)=1-\frac{4}{3}\frac{1}{s+1}+\frac{1}{3}\frac{1}{s-2},\quad\mathcal{R e}\{s\}>2
$$

或者

$$
X(s)=\frac{(s-1)^{2}}{(s+1)(s-2)},\mathcal{R}_{e}|_{s}|>2
$$

式中这个 ROC 是对 x(t) 的三项拉普拉斯变换都收敛的 s 值的集合。该例的零极点图及其 ROC 如图 9.3 所示。另外，因为 X(s) 的分子、分母同阶次，所以 X(s) 在无限远点既无极点，也无零点。

在(9.6)式已经提到，当 $ s = j\omega $ 时，拉普拉斯变换就是傅里叶变换。然而，如果这个拉普拉斯变换的 ROC 不包括 $ j\omega $ 轴 [即 $ \mathcal{R}\{s\} = 0\} $，那么傅里叶变换就不收敛。正如从图 9.3 中所看到的，事实上这就是例 9.5 的情况，这是与在 $ x(t) $ 中， $ \left(\frac{1}{3}\right)e^{2t}u(t) $ 这一项没有傅里叶变换是一致的。同时，从这个例子还看到，(9.35)式中的两个零点出现在同一个 s 值上。一般都用零点或极

![图像（物理页 500，第 1 幅）](../Figures/fig-p0500-01.jpg){#fig:p500-1}

**图 9.3 例 9.5 的零极点图和 ROC**

点标记的重复次数来指出它们的阶数。在例9.5中有一个二阶零点在s=1，和两个一阶极点分别在s=-1和s=2。在这个例子中，ROC位于最右边极点的右边。一般来说，对于一个

有理拉谱拉斯变换在极点位置和与一个给定的零极图有关的ROC之间存在一种紧密的关系，并且一些具体的限制都与 $ x(t) $的时域性质密切相关。下一节将来说明这些限制和有关的性质。

### 9.2 拉普拉斯变换收敛域 {#sec:9-2}

从前面的讨论已经看到，拉普拉斯变换的全部特性不仅要求 $ X(s) $ 的代数表示式，而且还应该伴随着收敛域的说明。这一点在例 9.1 和例 9.2 中体现得最为明显：两个很不相同的信号能够有完全相同的 $ X(s) $ 代数表示式，因此它们的拉普拉斯变换只有靠收敛域才能区分。这一节将说明对各种信号在 ROC 上的某些具体限制。将会看到，理解了这些限制往往使我们仅仅从 $ X(s) $ 的代数表示式和 $ x(t) $ 在时域中某些一般特征就能明确地给出或构成收敛域 ROC。

性质1： $ X(s) $的ROC在s平面内由平行于 $ j\omega $轴的带状区域所组成。

这一性质来自于这样一个事实： $ X(s) $ 的 ROC 是由这样一些 $ s = \sigma + j\omega $ 所组成，在那里 $ x(t)e^{-\sigma t} $ 的傅里叶变换收敛，也就是说， $ x(t) $ 的拉普拉斯变换的 ROC 是由这样一些 s 值组成的，对于这些 s 值， $ x(t)e^{-\sigma t} $ 是绝对可积的 $ ^{①} $，即

$$
\int_{-\infty}^{+\infty}\mid x(t)\mid e^{-\sigma}\mathrm{d}t<\infty
$$

因为这个条件只与 $ \sigma $，即 s 的实部有关，所以就得到性质 1。

性质2：对有理拉普拉斯变换来说，ROC内不包括任何极点。

这个性质，在到目前为止所研究的例子中都能很容易地看出。因为，在一个极点处， $ X(s) $为无限大，(9.3)式的积分显然在极点处不收敛，所以ROC内不能包括属于极点的s值。

性质3：如果 $ x(t) $ 是有限持续期，并且是绝对可积的，那么 ROC 就是整个 s 平面。

这个结果背后的直观性由图9.4和图9.5可以想到。这就是，一个有限持续期的信号具有这个性质，它在某一有限区间之外都是零，如图9.4所示。在图9.5(a)中画出了图9.4这样的 $ x(t) $乘以一个衰减的指数函数，而在图9.5(b)则画出同一类型的信号乘以一个增长的

指数函数。因为， $ x(t) $为非零的区间是有限长的，所以指数加权永远不会无界，这样 $ x(t) $的可积性不会由于这个指数加权而破坏就是合情合理的了。

性质3一个更加正规的证明如下：假设 $ x(t) $是绝对可积的，所以有

![图像（物理页 502，第 1 幅）](../Figures/fig-p0502-01.jpg){#fig:p502-1}

$$
\int_{T_{1}}^{T_{2}}\mid x(t)\mid\mathrm{d}t<\infty
$$

**图 9.4 有限持续期信号**

![图像（物理页 502，第 2 幅）](../Figures/fig-p0502-02.jpg){#fig:p502-2}

![图像（物理页 502，第 3 幅）](../Figures/fig-p0502-03.jpg){#fig:p502-3}

**(b)**

**图 9.5 (a) 有限持续期信号乘以衰减指数；(b) 有限持续期信号乘以增长指数**

对于在 ROC 内的 $ s = \sigma + j\omega $，就要求 $ x(t) \mathrm{e}^{-\alpha t} $ 是绝对可积的，即

$$
\int_{T_{1}}^{T_{2}}\mid x(t)\mid\mathrm{e}^{-\alpha t}\mathrm{d}t<\infty
$$

(9.37)式表明当 $ \mathcal{R}_{e}|s|=\sigma=0 $时的s是在ROC内。对于 $ \sigma>0 $， $ \mathrm{e}^{-\sigma t} $在 $ x(t) $为非零的区间内的最大值是 $ \mathrm{e}^{-\sigma T_{1}} $，因此可以写成

$$
\int_{T_{1}}^{T_{2}}\mid\boldsymbol{x}(t):\mathrm{e}^{-\sigma t}\mathrm{d}t<\mathrm{e}^{-\sigma T_{1}}\int_{T_{1}}^{T_{2}}\mid\boldsymbol{x}(t):\mathrm{d}t
$$

因为(9.39)式的右边是有界的，所以左边也就是有界的；因此对于 $ \mathcal{R}_{k}\{s\}>0 $的s平面必须也在ROC内。依类似的证明方法，若 $ \sigma<0 $，那么

$$
\int_{T_{1}}^{T_{2}}\mid\boldsymbol{x}(t)\mid\mathrm{e}^{-\sigma t}\mathrm{d}t<\mathrm{e}^{-\sigma T_{2}}\int_{T_{1}}^{T_{2}}\mid\boldsymbol{x}(t)\mid\mathrm{d}t
$$

$ x(t)e^{-\alpha t} $也是绝对可积的。因此，ROC包括整个s平面。

**例 9.6 设 $ x(t) $ 为**

$$
x(t)=\left\{\begin{aligned}&\mathrm{e}^{-at},&0<t<T\\ &0,& 其余 t\end{aligned}\right.
$$

那么其傅里叶变换 $ X(s) $

$$
X(s)=\int_{0}^{T}\mathrm{e}^{-a t}\mathrm{e}^{-s t}\mathrm{d}t=\frac{1}{s+a}\left[1-\mathrm{e}^{-(s+a)T}\right]
$$

在这个例子中，因为 $ x(t) $ 是有限长的，由性质 3，其 ROC 就是整个 s 平面。在 (9.42) 式中，形式上好像 $ X(s) $ 有一个极点在 s = -a，而这个根据性质 3 与 ROC 由整个 s 平面所组成是不一致的。然而，事实上 (9.42) 式的代数表示式中在 s = -a 都是分子和分母的零点！为了确定 s = -a 处的 $ X(s) $ 值，可以应用罗比塔法则而得

$$
\operatorname*{l i m}_{s\to-a}X(s)=\operatorname*{l i m}_{s\to-a}\left[\frac{\frac{\mathrm{d}}{\mathrm{d}s}(1-\mathrm{e}^{-(s+a)T})}{\frac{\mathrm{d}}{\mathrm{d}s}(s+a)}\right]=\operatorname*{l i m}_{s\to-a}T\mathrm{e}^{-a T}\mathrm{e}^{-s T}
$$

$$
\boldsymbol{X}\left(-a\right)=\boldsymbol{T}
$$

认识到在 $ x(t) $ 为非零的区间上保证指数型权函数是有界的这一点很重要，上面的讨论主要的就是依据这一事实： $ x(t) $ 是有限持续期的。下面两个性质要讨论有关这一结果的一种变形，即 $ x(t) $ 具有的有限范围仅仅在正时间或负时间方向上。

性质4：如果 $ x(t) $ 是右边信号，而且如果 $ \mathcal{R}_{0}\{s\} = \sigma_{0} $ 这条线位于 ROC 内，那么 $ \mathcal{R}_{0}\{s\} > \sigma_{0} $ 的全部 s 值都一定在 ROC 内。

若在某有限时间 $ T_{1} $ 之前， $ x(t)=0 $，则称该信号为右边信号，如图9.6所示。对于这样一个信号，有可能不存在任何 s 值，使其拉普拉斯变换收敛。一个例子就是 $ x(t)=\mathrm{e}^{t^{2}}u(t) $。然而，假如拉普拉斯变换对某一 $ \sigma $ 值收敛，譬如说 $ \sigma_{0} $，那么

![图像（物理页 503，第 1 幅）](../Figures/fig-p0503-01.jpg){#fig:p503-1}

$$
\int_{-\infty}^{+\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{0}t}\mathrm{d}t<\infty
$$

**图 9.6 右边信号**

或者，因为 $ x(t) $ 是右边信号，可等效为

$$
\int_{T_{1}}^{+\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{0}t}\mathrm{d}t<\infty
$$

如果 $ \sigma_{1} > \sigma_{0} $，由于随 $ t \to +\infty $， $ \mathrm{e}^{-\sigma_{1}t} $ 衰减得比 $ \mathrm{e}^{-\sigma_{0}t} $ 快，如图 9.7 所示，那么 $ x(t)\mathrm{e}^{-\sigma_{1}t} $ 也就一定绝对可积。正规一些，可以说，由于 $ \sigma_{1} > \sigma_{0} $，而有

$$
\begin{aligned}\int_{T_{1}}^{\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{1}t}\mathrm{d}t&=\int_{T_{1}}^{\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{0}t}\mathrm{e}^{-(\sigma_{1}-\sigma_{0})t}\mathrm{d}t\\&\leqslant\mathrm{e}^{-(\sigma_{1}-\sigma_{0})T_{1}}\int_{T_{1}}^{\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{0}t}\mathrm{d}t\end{aligned}
$$

因为 $ T_{1} $ 是有限值，根据(9.45)式，在(9.46)式不等式的右边就是有限的，所以 $ x(t)e^{-\sigma_{1}t} $ 就是绝对可积的。

应该注意到，在以上的证明中明显地是依赖于这一事实： $ x(t) $ 是右边信号。因而即使 $ \sigma_1 > \sigma_0 $，随着 $ t \to -\infty $， $ \mathrm{e}^{-\sigma_1 t} $ 发散快于 $ \mathrm{e}^{-\sigma_0 t} $，但是由于 $ t < T_1 $ 时， $ x(t) = 0 $， $ x(t)\mathrm{e}^{-\sigma_1 t} $ 在负的时间轴方向也不能无界地增长。同时，在这种情况下，如果有某一点 $ s $ 是在 ROC 内，那么所有位于这个 $ s $ 点右边的点，也就是所有具有更大实部的点，都在 ROC

![图像（物理页 503，第 2 幅）](../Figures/fig-p0503-02.jpg){#fig:p503-2}

**图9.7 若 $ x(t) $ 是右边信号，而 $ x(t)e^{-\sigma_{0}t} $ 是绝对可积的，那么 $ x(t)e^{-\sigma_{1}t} $， $ \sigma_{1} > \sigma_{0} $ 也一定绝对可积**

内。为此，这时一般就说 ROC 是在右半平面。

性质5：如果 $ x(t) $ 是左边信号，而且如果 $ \mathcal{R}_{e}\{s\}=\sigma_{0} $ 这条线位于 ROC 内，那么 $ \mathcal{R}_{e}\{s\}<\sigma_{0} $ 的全部 s 值也一定在 ROC 内。

若在某一有限时间 $ T_{2} $ 以后， $ x(t)=0 $，则称该信号为左边信号，如图9.8所示。这个性质的证明和直观性完全和性质4所做的相类似。同时，对于一个左边信号，如果有某一点 s 是在 ROC 内，那么所有位于这个 s 点左边的点也都在 ROC 内。因此一般就说 ROC 是在左半平面。

![图像（物理页 504，第 1 幅）](../Figures/fig-p0504-01.jpg){#fig:p504-1}

**图 9.8 左边信号**

性质6：如果 $ x(t) $ 是双边信号，而且如果 $ \mathcal{R}_0\{s\} = \sigma_0 $ 这条线位于 ROC 内，那么 ROC 就一定是由 s 平面的一条带状区域所组成，直线 $ \mathcal{R}_0\{s\} = \sigma_0 $ 位于带中。

一个双边信号就是对 t>0 和 t<0 都具有无限范围的信号，如果 9.9(a) 所示。对于这样一个信号，其收敛域 ROC 可以这样来求出：选取任一时间 $ T_{0} $，然而将 x(t) 分成右边信号

![图像（物理页 504，第 2 幅）](../Figures/fig-p0504-02.jpg){#fig:p504-2}

![图像（物理页 504，第 3 幅）](../Figures/fig-p0504-03.jpg){#fig:p504-3}

![图像（物理页 504，第 4 幅）](../Figures/fig-p0504-04.jpg){#fig:p504-4}

**图 9.9 双边信号分成右边信号和左边信号之和：**

$$
x(t);\mathrm{(b)}t<T_{0}
$$

$$
t>T_{0}
$$

$$
\iota>T_{0}
$$

$$
t<T_{0}
$$

$$
x(t)
$$

$x_{\mathrm{R}}(t)$ 和左边信号 $x_{\mathrm{L}}(t)$ 之和，如图 9.9(b) 和 (c) 所示。$x(t)$ 拉普拉斯变换的收敛域就是能使 $x_{\mathrm{R}}(t)$ 和 $x_{\mathrm{L}}(t)$ 两者的拉普拉斯变换都收敛的区域。根据性质 4，$\mathcal{L}\{x_{\mathrm{R}}(t)\}$ 的收敛域 ROC 对某 $\sigma_{\mathrm{R}}$ 值，由 $\mathcal{R}\{s\} > \sigma_{\mathrm{R}}$ 的半平面组成；而根据性质 5，$\mathcal{L}\{x_{\mathrm{L}}(t)\}$ 的 ROC 对某 $\sigma_{\mathrm{L}}$ 值，由 $\mathcal{R}\{s\}$

$ \langle\sigma_{L}\rangle $ 的半平面组成。 $ \mathcal{L}\{x(t)\} $ 的 ROC 就是这两个半平面的重叠部分，如图 9.10 所示。当然，这是假设 $ \sigma_{R}<\sigma_{L} $，因而这两半平面有某些重合。如果不是这种情况，那么即使 $ x_{R}(t) $ 和 $ x_{L}(t) $ 的拉普拉斯变换存在， $ x(t) $ 的拉普拉斯变换也不存在。

![图像（物理页 505，第 1 幅）](../Figures/fig-p0505-01.jpg){#fig:p505-1}

**(a)**

![图像（物理页 505，第 2 幅）](../Figures/fig-p0505-02.jpg){#fig:p505-2}

**(b)**

![图像（物理页 505，第 3 幅）](../Figures/fig-p0505-03.jpg){#fig:p505-3}

**(c)**

**图 9.10 (a) 图 9.9 中 $ x_{R}(t) $ 的 ROC; (b) 图 9.9 中 $ x_{L}(t) $ 的 ROC; (c) $ x(t)=x_{R}(t)+x_{L}(t) $的ROC，这里假定(a)和(b)中的ROC有重叠**

**例 9.7 设 $ x(t) $ 为**

$$
x(t)=\mathrm{e}^{-t|t|}
$$

对于 b>0 和 b<0 均如图 9.11 所示。因为这是一个双边信号，可将它分为右边信号和左边信号之和，即

$$
x(t)=\mathrm{e}^{-h}u(t)+\mathrm{e}^{+h}u(-i)
$$

由例9.1有

$$
\mathrm{e}^{-b\kappa}u(t){\leftrightarrow}\frac{1}{s+b},\quad\mathcal{R}\{s\}>-b
$$

由例9.2有

$$
\mathrm{e}^{+b t}u(-t){\overset{\mathcal{L}}{\leftrightarrow}}\frac{-1}{s-b},\quad\mathcal{R}_{b}\{s\}<+b
$$

虽然，(9.48)式中每一单独项的拉普拉斯变换都有一个收敛域，但如果 $ b\leq0 $，就没有公共的收敛域，

![图像（物理页 505，第 4 幅）](../Figures/fig-p0505-04.jpg){#fig:p505-4}

**图 9.11 b>0 和 b<0 时的信号 $ x(t)=\mathrm{e}^{-b,t} $**

于是对这样一些 b 值， $ x(t) $ 就没有拉普拉斯变换。如果 b>0， $ x(t) $ 的拉普拉斯变换是

$$
\mathrm{e}^{-b|t|}\xrightarrow{x}\frac{1}{s+b}-\frac{1}{s-b}=\frac{-2b}{s^{2}-b^{2}},\quad-b<\mathcal{R}\backslash s\}<+b
$$

相应的零极点图如图9.12所示，阴影区所指为ROC。

一个信号要么没有拉普拉斯变换，否则就一定属于由性质3到性质6这4类情况中的某一种。于是对具有某一拉普拉斯变换的信号而言，ROC一定是整个s平面(有限长信号)、某一左半平面(左边信号)、某一右半平面(右边信号)、或者一条带状收敛域(双边信号)等这4种中的一种。在所有已经讨论过的

![图像（物理页 506，第 1 幅）](../Figures/fig-p0506-01.jpg){#fig:p506-1}

**图 9.12 例 9.7 的零极点图及其 ROC**

例题中，收敛域 ROC 都有一个另外的性质，即：收敛域在每一个方向上（也就是 $ R_e\{s\} $ 增加和 $ R_e\{s\} $ 减小）都是被极点所界定，或者延伸到无限远。事实上，对有理拉普拉斯变换来说，这总是成立的：

性质7：如果 $ x(t) $ 的拉普拉斯变换 $ X(s) $ 是有理的，那么它的 ROC 是被极点所界定或延伸到无限远。另外，在 ROC 内不包含 $ X(s) $ 的任何极点。

对于这一性质的正规证明有些繁琐，但它基本上是由于如下事实的一个结果：一个具有有理拉普拉斯变换的信号均由指数信号的线性组合所构成，并且根据例9.1和例9.2，在该线性组合中，每一项变换的ROC一定有这一性质。作为性质7的一个结果，再与性质4和性质5结合在一起就有

性质8：如果 $ x(t) $ 的拉普拉斯变换 $ X(s) $ 是有理的，若 $ x(t) $ 是右边信号，则其 ROC 在 s 平面上位于最右边极点的右边；若 $ x(t) $ 是左边信号，则其 ROC 在 s 平面上位于最左边极点的左边。

为了说明不同的 ROC 如何与相同的零极点图相联系，考虑下面这个例子。

例 9.8 设有一拉普拉斯变换代数表示式为

$$
X(s)=\frac{1}{(s+1)(s+2)}
$$

其零极点图如图9.13(a)所示。正如在图9.13(b)~(d)所指出的，能与这个代数表示式有关的存在着三种可能的ROC，对应着三种不同的信号。与图9.13(b)零极点图有关的是右边信号。因为ROC包括jω轴，所以该信号的傅里叶变换收敛。图9.13(c)对应于一个左边信号，而图9.13(d)则对应一个双边信号。后面这两个信号当中没有一个傅里叶变换，因为它们的ROC都不包括jω轴。

![图像（物理页 507，第 1 幅）](../Figures/fig-p0507-01.jpg){#fig:p507-1}

**图 9.13 (a)例9.8的零极点图；(b)对应于右边信号的ROC; (c)对应于左边信号的ROC；(d)对应于双边信号的ROC**

### 9.3 拉普拉斯反变换 {#sec:9-3}

在9.1节讨论了把一个信号的拉普拉斯变换看作是该信号经指数加权后的傅里叶变换；也就是说，将 $ s $表示成 $ s = \sigma + j\omega $，一个信号 $ x(t) $的拉普拉斯变换是

$$
X(\sigma+\mathrm{j}\omega)=\mathcal{F}\{x(t)\mathrm{e}^{-\sigma t}\}=\int_{-\infty}^{+\infty}x(t)\mathrm{e}^{-\sigma t}\mathrm{e}^{-\mathrm{j}\omega t}\mathrm{d}t
$$

式中的 $ s = \sigma + j\omega $ 是在 ROC 中。可以利用(4.9)式的傅里叶反变换关系对(9.53)式求反变换为

$$
x(t)\mathrm{e}^{-\sigma t}=\mathcal{F}^{-1}\{X(\sigma+\mathrm{j}\omega)\}\nonumber=\frac{1}{2\pi}\int_{-\infty}^{+\infty}X(\sigma+\mathrm{j}\omega)\mathrm{e}^{\mathrm{j}\omega t}\mathrm{d}\omega
$$

或者将两边各乘以 $ e^{\alpha} $，可得

$$
x(t)=\frac{1}{2\pi}\int_{-\infty}^{+\infty}X(\sigma+\mathrm{j}\omega)\mathrm{e}^{(\sigma+\mathrm{j}\omega)t}\mathrm{d}\omega
$$

这就是说，可以这样从拉普拉斯变换中来恢复 $ x(t) $：在 ROC 内，将 $ \sigma $ 固定不变，在 $ \omega $ 从 $ -\infty $ 到 $ +\infty $ 变化的这一组 $ s = \sigma + j\omega $ 值上按 (9.55) 式求值。若将变量在 (9.55) 式中从 $ \omega $ 改变为 $ s $，并利用 $ \sigma $ 是常数这一点，可以将该式的意义更为突出，并从 $ X(s) $ 恢复 $ x(t) $ 中获得更深透的认识。因为 $ \sigma $ 为常数，所以 $ ds = j d\omega $，可得拉普拉斯反变换的基本关系式为

$$
\boxed{x(t)=\frac{1}{2\pi\mathrm{j}}\int_{\sigma-\mathrm{i}\infty}^{\sigma+\mathrm{j}\infty}X(s)\mathrm{e}^{s}\mathrm{d}s}
$$

该式说明， $ x(t) $ 可以用一个复指数信号的加权积分来表示。(9.56) 式的积分路径是在 s 平面内对应于满足 $ \mathcal{R}\{s\}=\sigma $ 的全部 s 点的这条直线，该直线平行于 jω 轴。再者，在 ROC 内可以

选取任何这样一根直线；也就是说，在 ROC 内可以选取任何 $ \sigma $ 值，而使 $ X(\sigma + j\omega) $ 收敛。对于一般的 $ X(s) $ 来说，这个积分的求值要求利用复平面的围线积分，在此不作讨论。然而，对于有理变换，求其拉普拉斯反变换用不着直接计算(9.56)式，而可以像在第 4 章求傅里叶反变换所做的那样，采用部分分式展开的办法来求。这一过程基本上就是把一个有理的代数表示式展开成低阶次项的线性组合。

例如，假设没有重阶极点，并假设分母多项式的阶高于分子多项式的阶，那么 $ X(s) $ 就可以展开为如下形式：

$$
X(s)=\sum_{i=1}^{m}\frac{A_{i}}{s+a_{i}}
$$

根据 $ X(s) $ 的收敛域 ROC，在该式中每一项的 ROC 都能推演出来，然后由例 9.1 和例 9.2，每一项的拉普拉斯反变换都可被确定。在 (9.57) 式中每一项 $ A_i/(s+a_i) $ 的反变换都有两种可能的选择，若 ROC 是位于极点 $ s = -a_i $ 的右边，那么这一项的反变换就是 $ A_i e^{-a_i t} u(t) $，是一个右边信号；若 ROC 是位于极点 $ s = -a_i $ 的左边，那么这一项的反变换就是 $ -A_i e^{-a_i t} u(-t) $，是一个左边信号。将 (9.57) 式中每一项的反变换相加，就得到 $ X(s) $ 的反变换。详细过程最好通过几个例子来给出。

**例9.9 设有 $ X(s) $为**

$$
X(s)=\frac{1}{(s+1)(s+2)},\mathcal{R}_{s}|_{s}|>-1
$$

为了求它的反变换，先对它进行部分分式展开为

$$
\begin{aligned}X(s)&=\frac{1}{(s+1)(s+2)}\\&=\frac{A}{s+1}+\frac{B}{s+2}\quad()\end{aligned}
$$

根据附录介绍的办法，将(9.59)式两边各乘以 $ (s+1)(s+2) $。然后令两边同s方次的系数相等，可求出系数A和B。另一种方法是利用下列关系：

$$
\boldsymbol{A}=\left[\left(s+1\right)\boldsymbol{X}(s)\right]|_{s=-1}=1
$$

$$
\boldsymbol{B}=\left[\left(s+2\right)\boldsymbol{X}(s)\right]|_{s=-2}=-1
$$

由此， $ X(s) $的部分分式展开式为

$$
X(s)=\frac{1}{s+1}-\frac{1}{s+2}
$$

由例9.1和例9.2可知，根据ROC是位于极点的左边还是右边，对于

![图像（物理页 508，第 1 幅）](../Figures/fig-p0508-01.jpg){#fig:p508-1}

**(a)**

![图像（物理页 508，第 2 幅）](../Figures/fig-p0508-02.jpg){#fig:p508-2}

**(b)**

![图像（物理页 508，第 3 幅）](../Figures/fig-p0508-03.jpg){#fig:p508-3}

**(c)**

**图 9.14 例 9.8X(s) 的部分分式展开式中每一项 ROC 的构成：**

(a)X(s)的零极图和ROC;

(b)在 s = -1 的极点及其 ROC;

(c)在 s = -2 的极点及其 ROC

$ 1/(s+a) $ 都有两种可能的反变换，因此就需要确定与(9.62)式中每个一次项有关的 ROC。这个可

以参照9.2节所建立的ROC性质来完成。因为 $ X(s) $的ROC是 $ \mathcal{R}\{s\}>-1 $，那么(9.62)式中的每一项的ROC都应包括 $ \mathcal{R}\{s\}>-1 $。然后，对于每一项来说，其ROC就可以向左或向右（或向两边）延伸，直到被一个极点所界定或至无限远为止，这就如图9.14所示。图9.14(a)是由(9.58)式给出的 $ X(s) $的零极点图和ROC，而图9.14(b)和(c)就是(9.62)式中每一项的零极点图及其ROC。总的ROC在图中用阴影区表示。由图9.14(c)所代表的这一项，其ROC还可以向左延伸如图示，直至被一个极点所界定。

因为 ROC 是位于这两个极点的右边，所以如同在图 9.14(b) 和 (c) 中所看到的，这两个单独项中的每一项的 ROC 也就应在各自极点的右边，结果根据前一节的性质 8 可知，它们都对应于右边信号。由例 9.1，(9.62) 式中每一项的反变换就是

$$
\mathrm{e}^{-t}u(t){\overset{\mathcal{Z}}{\leftrightarrow}}\frac{1}{s+1},\quad\mathcal{R e}\{s\}>-1
$$

$$
\mathrm{e}^{-2t}u(t){\stackrel{\mathcal{X}}{\leftrightarrow}}{\frac{1}{s+2}},\quad\mathcal{R}_{t}\{s\}|>-2
$$

由此可得

$$
[\mathrm{e}^{-t}-\mathrm{e}^{-2t}]u(t){\overset{\mathcal{X}}{\longleftrightarrow}}\frac{1}{(s+1)(s+2)},\quad\mathcal{R}_{\bullet}|_{S}|>-1
$$

例 9.10 现在假设 $ X(s) $ 的代数表示式仍由 (9.58) 式给出，但 ROC 是在 $ \mathbb{R}_+ \backslash s\} < -2 $ 的左半平面。 $ X(s) $ 的部分分式展开仅与它的代数表示式有关，所以 (9.62) 式仍然不变。然而，由于这个新的 ROC 是位于两个极点的左边，所以 (9.62) 式中每一项的 ROC 也都必须位于极点的左边。这就是说，对应于极点 s = -1 这一项的 ROC 是 $ \mathbb{R}_+ \backslash s\} < -1 $；而对应于极点 s = -2 这一项的 ROC 是 $ \mathbb{R}_+ \backslash s\} < -2 $。那么，根据例 9.2 就有

$$
-\mathrm{~e~}^{-t}u(-\mathrm{~}t\mathrm{)~}{\overset{\mathcal{L}}{\leftrightarrow}}\frac{1}{s+1},\quad\mathcal{R}_{\bullet}\{s\}<-1
$$

$$
-\mathrm{e}^{-2t}u(-t)^{\stackrel{\mathcal{A}}{\leftrightarrow}}\frac{1}{s+2},\quad\mathcal{R}_{\ast}\vert_{s}\}<-2
$$

所以有

$$
x(t)=\left[-\mathrm{e}^{-t}+\mathrm{e}^{-2t}\right]u(-t){\overset{\mathcal{L}}{\leftrightarrow}}\frac{1}{(s+1)(s+2)},\quad\mathcal{R}_{e}\{s\}<-2
$$

例9.11 最后，假设(9.58)式的 $ X(s) $，其ROC是 $ -2<R_{0}\}\leq-1 $，这时的ROC是在s=-1极点的左边，所以对应于这一项的就是如(9.66)式的左边信号；而ROC是在s=-2极点的右边，所以这一项就对应于(9.64)式的右边信号。将两者合在一起求得

$$
x(t)=-\mathrm{e}^{-t}u(-t)-e^{-2t}u(t)\xrightarrow[t\to\infty]{x}\frac{1}{(s+1)(s+2)},\quad-2<\mathcal{R}_{*}\{s\}<-1
$$

正如在附录中所讨论的，当 $ X(s) $有重阶极点，或者分母的阶不是高于分子的阶时，部分分式展开式中除了在例9.9到例9.11中考虑的一次项外，还应包括其它的项。到9.5节，当讨论完拉普拉斯变换的性质以后，还将讨论其它一些拉普拉斯变换对，连同拉普拉斯变换的性质一起，就能够将例9.9所给出的求反变换的方法推广到任意有理变换中去。

### 9.4 由零极点图对傅里叶变换进行几何求值 {#sec:9-4}

在9.1节已经看到，一个信号的傅里叶变换就是拉普拉斯变换在 $ j\omega $轴上的求值。这一节

将讨论由与一个有理拉普拉斯变换有关的零极点图来求傅里叶变换的一种求值方法，并且更一般地说，求拉普拉斯在任意 s 点上的值的几何求值法。为了建立这一方法，首先考虑只有一个单个零点的拉普拉斯变换[即， $ X(s)=(s-a) $]在某一给定的 s，如 $ s=s_{1} $ 处求值。这个代数表示式 $ s_{1}-a $ 是两个复数的和，一个是 $ s_{1} $，另一个是 $ -a $；它们中的每一个都能在复平面内用一个向量来表示，如图 9.15 所示。然后，代表这个复数 $ (s_{1}-a) $ 的向量就是向量 $ s_{1} $ 和 $ -a $ 之和；在图 9.15 中可以看出，这个向量就是从 $ s=a $ 这个零点到点 $ s_{1} $ 的向量 $ s_{1}-a $。这样， $ X(s_{1}) $ 的模就是这个向量的长度，而相位就是这个向量对于实轴的角度。如果 $ X(s) $ 在 $ s=a $ 是一个极点[即： $ X(s)=1/(s-a) $]，那么 $ X(s) $ 的分母就是上面讨论的同一向量，这时 $ X(s_{1}) $ 的模是该向量（从极点 s=a 到 s=s_{1} 点）长度的倒数，而相位则是该向量相对于实轴角度的负值。

一个更一般的有理拉普拉斯变换是由上述讨论的零点和极点项的乘积所组成，也就是说，一个有理的拉普拉斯变换可以因式分解成

$$
X(s)=M\frac{\prod_{i=l}^{R}(s}{\prod_{j=l}^{P}(s-\frac{\beta_{i}}{\alpha_{j}})}
$$

为了求取 $ X(s) $ 在 $ s=s_{1} $ 的值，乘积中的每一项都可用一个从零点或极点到 $ s_{1} $ 点的向量来表示。那么， $ X(s_{1}) $ 的模就是各零点向量（从各个零点到 $ s_{1} $ 的向量）长度乘积的 M 倍被各极点向量（从各个极点到 $ s_{1} $ 的向量）长度的积相除，而复数 $ X(s_{1}) $ 的相角则是这些零点向量相角的和减去这些极点向量相角的和。如果在 (9.70) 式中比例因子 M 是负的，则对应有一个附加相角 $ \pi $。如果 $ X(s) $ 有多阶极点或零点（或均有），即相应于某些 $ \alpha_{i} $ 或/和 $ \beta_{i} $ 是相等的，那么这些多阶极点或零点向量的长度和相角在 $ X(s_{1}) $ 中都应包括相应的倍数（等于极点或零点的阶）。

$$
X(s)=\frac{1}{s+\frac{1}{2}},\quad\mathcal{R}_{\bullet}\{s\}>-\frac{1}{2}
$$

**例 9.12 有一 $ X(s) $ 为**

$$
X(j\omega)=\frac{1}{j\omega+1/2}
$$

$ X(s)|_{s=j\omega} $ 就是傅里叶变换，故该例的傅里叶变换就是

$ X(s) $的零极点图如图9.16所示。为了用几何法确定傅里叶变换，在图中构造了一个极点向量。傅里叶变换在频率 $ \omega $处的模，就是从极点到虚轴上 $ j\omega $点向量长度的倒数，而傅里叶变换的相位就是该向量相角的负值。由图9.16，从几何上可写出

$$
X(\mathrm{j}\omega)^{2}=\frac{1}{\omega^{2}+(1/2)^{2}}
$$

![图像（物理页 510，第 1 幅）](../Figures/fig-p0510-01.jpg){#fig:p510-1}

$$
\prec X(\mathrm{j}\omega)=-\tan^{-1}2\omega
$$

**图 9.15 分别代表复数 $ s_{1} $，-a 和 $ (s_{1}-a) $ 的向量 $ s_{1} $，-a 和 $ s_{1}-a $ 的复平面表示**

和

![图像（物理页 510，第 2 幅）](../Figures/fig-p0510-02.jpg){#fig:p510-2}

**图9.16 例9.12的零极点图。 $ \left|X(j\omega)\right| $ 就是图示向量长度的倒数， $ \left\langle X(j\omega)\right. $ 是向量相角的负值**

傅里叶变换几何确定的价值往往在于用它来近似观察整体特性。例如，在图9.16中很快能看出，极点向量的长度随 $ \omega $的增加而单调增加，因此傅里叶变换的模将随 $ \omega $的增加而单调下降。由零极点图对傅里叶变换特性作出一般性结论的能力将考虑用一阶和二阶系统作为例子给予进一步的说明。

#### 9.4.1 一阶系统 {#sec:9-4-1}

作为例9.12的一般化，现在来考虑曾在6.5.1节较详细讨论过的一阶系统。这类系统的单位冲激响应是

$$
h\left(t\right)=\frac{1}{\tau}\mathrm{e}^{-t/\tau}u\left(t\right)
$$

它的拉普拉斯变换就是

$$
H(s)=\frac{1}{s\tau+1},\quad\mathcal{R}_{e}\{s\}>-\frac{1}{\tau}
$$

其零极点图如图9.17所示。从该图可以看到，极点向量的长度在 $ \omega=0 $最短，并随 $ \omega^{\textcircled{1}} $增加而单调增加；同时，极点向量的相角随 $ \omega $从0增加到 $ \infty $而单调地从0增加到 $ \pi/2 $。

![图像（物理页 511，第 1 幅）](../Figures/fig-p0511-01.jpg){#fig:p511-1}

**图 9.17 (9.76) 式一阶系统的零极点图**

![图像（物理页 511，第 2 幅）](../Figures/fig-p0511-02.jpg){#fig:p511-2}

从极点向量随 $ \omega $ 变化的规律来看，很明显其频率响应 $ H(j\omega) $ 的模随 $ \omega $ 增加而单调下降，而 $ \left\langle H(j\omega)\right\rangle $ 则单调地从 0 下降到 $ -\pi/2 $，如图 9.18 该系统的波特图所示。同时也注意到，当 $ \omega = 1/\tau $ 时，极点向量的实部和虚部相等，从而频率响应的模从它在 $ \omega = 0 $ 时的最大值下降了

![图像（物理页 511，第 3 幅）](../Figures/fig-p0511-03.jpg){#fig:p511-3}

**图 9.18 一阶系统的频率响应**

1/ $ \sqrt{2} $，或近似下降 3dB；而此时频率响应的相位是 $ \pi/4 $ 值。这是与 6.5.1 节讨论一阶系统所得结论相一致的，在那里就将 $ \omega = 1/\tau $ 称之为 3dB 点或折转频率，也就是 $ |H(j\omega)| $ 波特图的直线近似在斜率上有一个转折处的频率。在 6.5.1 节也看到，时间常数 $ \tau $ 控制了一阶系统的响应速度，而现在看到，这样一个系统在 $ s = -1/\tau $ 的极点是在负的实轴上，它到原点的距离就是该时间常数的倒数。

从图形的说明上也能看到，时间常数，或者等效地说 $ H(s) $ 极点位置的变化是如何改变一阶系统的特性的。特别是，极点愈朝左半面移，系统的折转频率，或有效截止频率就增加；同时，由(9.75)式和图6.19都可看到，极点向左移动对应于时间常数的减小，结果单位冲激响应就衰减得更快，而阶跃响应则有一个更快的上升时间。极点位置的实部和系统响应速度之间的这一关系一般总是成立的，即远离 $ j\omega $轴的那些极点，总是对应于单位冲激响应中那些快速响应项。

#### 9.4.2 二阶系统 {#sec:9-4-2}

下面来讨论二阶系统，该系统也曾在6.5.2节较为详细地讨论过。对于这类系统的单位冲激响应和频率响应原先分别由(6.37)式和(6.33)式给出为

$$
h\left(t\right)=M\left[\mathrm{e}^{c_{1}t}-\mathrm{e}^{c_{2}t}\right]u\left(t\right)
$$

式中

$$
\begin{aligned}&c_{1}=-\zeta\omega_{n}+\omega_{n}\sqrt{\zeta^{2}-1}\\&c_{2}=-\zeta\omega_{n}-\omega_{n}\sqrt{\zeta^{2}-1}\\&M=\frac{\omega_{n}}{2\sqrt{\zeta^{2}-1}}\\ \end{aligned}
$$

以及

$$
H(\mathrm{j}\omega)=\frac{\omega_{n}^{2}}{(\mathrm{j}\omega)^{2}+2\zeta\omega_{n}(\mathrm{j}\omega)+\omega_{n}^{2}}
$$

单位冲激响应的拉普拉斯变换是

$$
H(s)=\frac{\omega_{n}^{2}}{s^{2}+2\zeta\omega_{n}s+\omega_{n}^{2}}=\frac{\omega_{n}^{2}}{(s-c_{1})(s-c_{2})}.
$$

若 $ \zeta>1 $， $ c_1 $ 和 $ c_2 $ 都是实数，因此两个极点都位于实轴上，如图 9.19(a) 所示。 $ \zeta>1 $ 的情况实质上就是如在 9.4.1 节讨论的两个一次项的乘积。因此在这种情况下， $ |H(j\omega)| $ 随着 $ |\omega| $ 的增加而单调下降，而 $ \zeta H(j\omega) $ 则由 $ \omega=0 $ 时为 0 变到 $ \omega\to\infty $ 时的一 $ \pi $。这点可从图 9.19(a) 得到证实，因为这两个极点中的每一个到点 $ j\omega $ 的向量长度都随 $ \omega $ 的增加而单调增加，而每个极点向量的相角则随 $ \omega $ 从 0 到 $ \infty $ 的增加相应地从 0 增加到 $ \pi/2 $。同时也注意到，随着 $ \zeta $ 的增加，一个极点移向 $ j\omega $ 轴（这就是在单位冲激响应中反映衰减较慢的一项）；而另一个极点则愈向左半面移（这就是在单位冲激响应中反映衰减较快的一项）。于是，在大的 $ \zeta $ 值下，正是紧靠 $ j\omega $ 轴的这一极点支配着系统的响应。同样，从图 9.19(b) 所示的在 $ \zeta\gg1 $ 下的极点向量来考虑，在低的频率部分，紧靠 $ j\omega $ 轴的极点向量的长度和相角随 $ \omega $ 的变化，比远离 $ j\omega $ 轴的极点向量要灵敏得多，所以在低频区域，频率响应特性主要地受紧靠 $ j\omega $ 轴极点的影响。

若 $ 0<\zeta<1,c_{1} $ 和 $ c_{2} $ 都是复数，所以零极点图如图 9.19(c) 所示。相应地，单位冲激响应

![图像（物理页 513，第 1 幅）](../Figures/fig-p0513-01.jpg){#fig:p513-1}

**图 9.19 (a) $ \zeta>1 $ 时二阶系统的零极点图；(b) $ \zeta\gg1 $ 时的极点向量；**

(c)0< $ \zeta $<1时二阶系统的零极点图；

(d)0< $ \zeta $<1时， $ \omega=\omega_{n}\sqrt{1-\zeta^{2}} $和 $ \omega=\omega_{n}\sqrt{1-\zeta^{2}}\pm\zeta\omega_{n} $的极点向量

和阶跃响应都有振荡的部分。应该注意到，这两个极点是发生在复数共轭的位置上。事实上，由9.5.5节的讨论可知，对于一个实值信号而言，复数极点(和零点)总是共轭成对地出现的。从这个图上，特别是当 $ \zeta $较小时，这些极点是很靠近 $ j\omega $轴的，随着 $ \omega $接近于 $ \omega_n\sqrt{1-\zeta^2} $，频率响应特性主要是由第二象限内的这个极点所决定的。尤其是，在 $ \omega = \omega_n\sqrt{1-\zeta^2} $时，这个极点向量的长度有一个最小值，因此，定性地可以预期到，频率响应的模在该频率附近应有一个峰值。由于有其它极点的存在，峰值不是真正出现在 $ \omega = \omega_n\sqrt{1-\zeta^2} $处，而是在略比它小一点的频率上。图9.20(a)对于 $ \omega_n = 1 $和几个不同的 $ \zeta $值下，仔细地画出了频率响应的模，很明显，在极点附近有一个所期望的特性。当然，这与6.5.2节对二阶系统所作的分析是一致的。

因此，对于 $ 0 < \zeta < 1 $，这个二阶系统是一个非理想的带通滤波器，参数 $ \zeta $ 控制着频率响应的尖锐程度和峰值的宽度。从图 9.19(d) 的几何性质上也可看到，当频率 $ \omega $ 在 $ \omega_n \sqrt{1 - \zeta^2} $ 上下各增减一个 $ \zeta\omega_n $ 的值时，第二象限极点向量的长度对于 $ \omega = \omega_n \sqrt{1 - \zeta^2} $ 处的最小值来说

就增加了 $ \sqrt{2} $倍，这样，对于小的 $ \zeta $值来说，远在第三象限的极点，其影响可以忽略， $ |H(j\omega)| $在频率范围

$ \omega_{n}\sqrt{1-\zeta^{2}}-\zeta\omega_{n}<\omega<\omega_{n}\sqrt{1-\zeta^{2}}+\zeta\omega_{n} $ 内就在其峰值 $ 1/\sqrt{2} $ 之内。若定义相对带宽 B 为这个频率间隔（即 $ 2\zeta\omega_{n} $）除以自然频率 $ \omega_{n} $，则有

$$
B\;=\;2\upzeta
$$

因此， $ \zeta $ 愈接近于零，频率响应的峰值就愈尖锐，峰值宽度就愈窄。另外，B 就是在6.5.2节定义的二阶系统品质因数 Q 值的倒数，因此随着品质因数的增加，相对带宽减小，滤波器的频率选择性就愈强。

对于 $ \omega_n = 1 $ 和几个不同的 $ \zeta $ 值下，该二阶系统的相位特性如图 9.20(b) 所示。由图 9.19(d) 可以看到，第二象限极点向量的相角在频率 $ \omega $ 由 $ \omega_n \sqrt{1 - \zeta^2} - \zeta \omega_n $ 变到 $ \omega_n \sqrt{1 - \zeta^2} $ 再变到 $ \omega_n \sqrt{1 - \zeta^2} + \zeta \omega_n $ 的过程中，由 $ -\pi/4 $ 到 0 再到 $ \pi/4 $ 内变化。对于较小的 $ \zeta $ 值，第三象限极点向量的相角在这个频率范围内的变化很小，其结果就是在这个频率间隔上， $ \langle H(\omega) \rangle $ 就是一个 $ \pi/2 $ 的急剧变化。这就是在图 9.20(b) 中所指出的。

$\zeta$ 固定而改变 $\omega_n$，在上面的讨论中仅改变了频率坐标的尺度，也就是说，$|H(j\omega)|$ 和 $\zeta H(j\omega)$ 仅仅取决于 $\omega/\omega_n$。从图 9.19(c) 中也能够很容易地确定，当保持 $\omega_n$ 不变而变化 $\zeta$ 时，这些极点和系统特性是如何随 $\zeta$ 而改变的。因为 $\cos\theta = \zeta$，所以这两个极点

![图像（物理页 514，第 1 幅）](../Figures/fig-p0514-01.jpg){#fig:p514-1}

**(a)**

![图像（物理页 514，第 2 幅）](../Figures/fig-p0514-02.jpg){#fig:p514-2}

**图 9.20 0<ζ<1 时，二阶系统频率响应： (a) 模特性；(b) 相位特性**

就沿着半径为 $ \omega_{n} $ 的半圆移动。当 $ \zeta=0 $ 时，这两个极点都在虚轴上，这就对应于在时域中单位冲激响应是无衰减的正弦振荡。随着 $ \zeta $ 从 0 增加到 1，这两个极点仍为复数，并移向左半面，而且从原点到这两个极点的向量长度保持为常数 $ \omega_{n} $。随着极点的实部变得更负，有关的时间响应随 $ t\to\infty $ 就衰减得更快。同时，如同已经看到的，随着 $ \zeta $ 从 0 朝 1 增加的过程中，频率响应的相对带宽也随着增加，频率响应的尖锐程度渐渐降低，频率选择性变差。

#### 9.4.3 全通系统 {#sec:9-4-3}

作为利用频率响应几何求值的最后一个例子，我们来考虑一个系统，其单位冲激响应的拉普拉斯变换有如图9.21(a)所示的零极点图。由该图可明显看出，沿着 $ j\omega $轴的任何一点，

其极点向量和零点向量的长度都是相等的，结果，频率响应的模是一个常数而与频率无关。这样的系统称为全通系统，因为它等增益（或等衰减）地通过所有频率。频率响应的相位是 $ \theta_{1}-\theta_{2} $，或者因为 $ \theta_{1}=\pi-\theta_{2} $，所以

$$
\prec H(\mathrm{j}\omega)=\pi-2\theta_{2}
$$

由图9.21(a)可知， $ \theta_{2}=\tan^{-1}(\omega/a) $，因此

$$
\prec H(\mathrm{j}\omega)=\pi-2\tan^{-1}\left(\frac{\omega}{a}\right)
$$

$ H(j\omega) $的模和相位特性均如图9.21(b)所示。

![图像（物理页 515，第 1 幅）](../Figures/fig-p0515-01.jpg){#fig:p515-1}

**(a)**

![图像（物理页 515，第 2 幅）](../Figures/fig-p0515-02.jpg){#fig:p515-2}

![图像（物理页 515，第 3 幅）](../Figures/fig-p0515-03.jpg){#fig:p515-3}

**(b)**

**图 9.21 (a) 全通系统的零极点图；(b) 全通系统频率响应的模和相位特性**

### 9.5 拉普拉斯变换的性质 {#sec:9-5}

在傅里叶变换的应用中，主要是依赖于在4.3节所获得的一组性质。这一节，将考虑相应的一组拉普拉斯变换的性质。很多结果的导出都和傅里叶变换中相应性质的导出相类似，因此将不作详细推导，有些将在本章末习题中留作作业（见习题9.52到9.54）。

#### 9.5.1 线性 {#sec:9-5-1}

若

$$
x_{1}(t)\xrightarrow{\mathcal{L}}X_{1}(s),\quad\mathrm{ROC} 为 R_{1}
$$

和

$$
x_{2}(t)\xleftrightarrow{\mathcal{L}}X_{2}(s),\quad\mathrm{ROC} 为 R_{2}
$$

则

$$
a x_{1}(t)+b x_{2}(t)\stackrel{\mathcal{L}}{\leftrightarrow}a X_{1}(s)+b X_{2}(s),\quad\mathrm{R O C} 包括 R_{1}\cap R_{2}
$$

正如所指出的， $ X(s) $ 的收敛域至少是 $ R_1 $ 和 $ R_2 $ 的相交，这个交可以是空的；若是这样， $ X(s) $ 就没有收敛域，也即， $ x(t) $ 不存在拉普拉斯变换。例如，例 9.7 中 (9.47) 式的 $ x(t) $，在 b>0 时， $ X(s) $ 的 ROC 就是在和式中这两项 ROC 的交。若 b<0，在 $ R_1 $ 和 $ R_2 $ 中没有公共的点，即这个交是空的，因此， $ x(t) $ 就没有拉普拉斯变换。 $ X(s) $ 的 ROC 也可能比这个“交”大。作为一个简单例子，如 $ x_1(t)=x_2(t) $，且 a=-b，则在 (9.82) 式中 $ x(t)=0 $，因此 $ X(s)=0 $，这样 $ X(s) $ 的 ROC 就是整个 s 平面。

与一些项的线性组合相联系的 ROC，总可以利用在 9.2 节所得到的关于 ROC 的性质来构成。具体说来就是，根据这些单个项 ROC 的公共相交部分（假定各单项 ROC 有相交部分），就能找到一条线或一个带状区域是在这个线性组合的 ROC 当中，然后将其向右延伸 $ (\mathcal{R}_l \setminus s) $ 增加）和向左延伸 $ (\mathcal{R}_l \setminus s| $ 减小），直到最近的极点（这个极点也可能在无限远）为止。

例 9.13 这个例子要说明一个由信号的线性组合构成的信号，其拉普拉斯变换的 ROC 有时可能会延伸到超过这些单个项 ROC 的交。考虑信号

$$
x(t)=x_{1}(t)-x_{2}(t)
$$

这里 $ x_{1}(t) $ 和 $ x_{2}(t) $ 的拉普拉斯变换分别是

$$
X_{1}(s)=\frac{1}{s+1},\quad\mathcal{R}\{s\}>-1
$$

和

$$
X_{2}(s)=\frac{1}{(s+1)(s+2)},\quad\mathcal{R}_{e}\{s\}>-1
$$

$ X_{1}(s) $ 和 $ X_{2}(s) $ 的零极点图，包括 ROC 如图 9.22(a) 和 (b) 所示。由 (9.82) 式

$$
X(s)=\frac{1}{s+1}-\frac{1}{(s+1)(s+2)}=\frac{s+1}{(s+1)(s+2)}=\frac{1}{s+2}
$$

由此，在 $ x_{1}(t) $和 $ x_{2}(t) $的线性组合中，在s=-1的极点被s=-1的零点所抵消。 $ X(s)=X_{1}(s) $

![图像（物理页 516，第 1 幅）](../Figures/fig-p0516-01.jpg){#fig:p516-1}

**(a)**

**(b)**

**(c)**

**图 9.22 例 9.13 的零极点图和 ROC: (a) $ X_{1}(s) $; (b) $ X_{2}(s) $;**

(c) $ X_{1}(s)-X_{2}(s) $。 $ X_{1}(s)-X_{2}(s) $的ROC包括 $ R_{1} $和 $ R_{2} $的交，这个交可以延伸到被极点s=-2界定为止

$ -X_2(s) $的零极点图如图9.22(c)所示。 $ X_1(s) $和 $ X_2(s) $的ROC的交是 $ \mathcal{R}\{s\} > -1 $。然而，因为ROC总是被一个极点或无限远点所界定，对这个例子来说， $ X(s) $的ROC就能够再向左延伸，直至被 $ s = -2 $的极点所界定为止，这就是由于在 $ s = -1 $零极点抵消的结果。

#### 9.5.2 时移性质 {#sec:9-5-2}

若

$$
x(t){\stackrel{\mathcal{X}}{\leftrightarrow}}X(s)\qquad\mathrm{R O C}=R
$$

则

$$
\boxed{x(t-t_{0}){\overset{\mathcal{L}}{\leftrightarrow}}e^{-s t_{0}}X(s),\quad \mathrm{~R O C}=R}
$$

#### 9.5.3 s 域平移 {#sec:9-5-3}

若

$$
x(t){\overset{\mathcal{F}}{\leftrightarrow}}X(s)\qquad\mathrm{R O C}=R
$$

则

$$
e^{s_{0}t}x(t)^{\frac{\mathcal{L}}{\leftrightarrow}}X(s-s_{0}),\quad\mathrm{R O C}=R+\mathcal{R}_{e}|_{s_{0}}|
$$

这就是说， $ X(s-s_0) $的ROC是 $ X(s) $的ROC平移一个 $ \mathcal{R}_0\{s_0\} $。于是，对于位于R中的任何一个s值， $ s+\mathcal{R}_0\{s_0\} $的值一定在 $ R_1 $中，如图9.23所示。应该注意，如果 $ X(s) $有一个极点或零点在s=a，那么 $ X(s-s_0) $就有一个极点或零点在 $ s-s_0=a $，也就是 $ s=a+s_0 $。

![图像（物理页 517，第 1 幅）](../Figures/fig-p0517-01.jpg){#fig:p517-1}

**(a)**

![图像（物理页 517，第 2 幅）](../Figures/fig-p0517-02.jpg){#fig:p517-2}

**(b)**

**图 9.23 s 域平移在 ROC 上的影响: (a) $ X(s) $ 的 ROC; (b) $ X(s - s_{0}) $ 的 ROC**

(9.88)式一个重要的特殊情况是当 $ s_{0}=j\omega_{0} $ 时，也就是当一个信号 $ x(t) $ 被用来调制一个周期复指数信号 $ e^{j\omega_{0}t} $ 时，这时(9.88)式就变成

$$
\begin{array}{r}{\mathrm{e}^{\mathrm{j}\omega_{0}t}x(t)^{\stackrel{\mathcal{L}}{\leftrightarrow}}X(s-\mathrm{j}\omega_{0}),\quad\mathrm{~R O C}=R}\end{array}
$$

(9.89)式的右边可以看作是在s平面内平行于实轴的一个平移，这就是说，若 $ x(t) $的拉普拉斯变换在s=a有一个极点或零点，那么 $ \mathrm{e}^{\mathrm{j}\omega}v^{t}x(t) $就在 $ s=a+\mathrm{j}\omega $。有一个极点或零点。

#### 9.5.4 时域尺度变换 {#sec:9-5-4}

若

$$
x(t){\overset{\mathcal{X}}{\leftrightarrow}}X(s)\qquad\mathrm{R O C}=R
$$

则

$$
\boxed{x\left(a t\right)\xrightarrow{\mathcal{L}}\frac{1}{\mid a\mid}X\left(\frac{s}{a}\right),\qquad\mathrm{ROCR}_{1}=\frac{R}{a}}
$$

这就是说，对于在 $R$ 中任何 $s$ 值[如图 9.24(a) 所示]，$s/a$ 的值一定位于 $R_1$ 中，如图 9.24(b) 所示，这里 $a>1$。注意：对于 $a>1$，$X(s)$ 的 ROC 要压缩一个 $1/a$ 的倍数，如图 9.24(b) 所示；而对于 $0<a<1$，ROC 要扩展一个 $1/a$ 的倍数。另外，(9.90)式还意味着，若 $a$ 为负，ROC 要受到一个倒置再加一个尺度变换。这就是如图 9.24(c) 所示，该图是对应于 $0>a>-1$ 的情况，$1/|a|X(s/a)$ 的 ROC 涉及到关于 $j\omega$ 轴的反转，再加上一个 $1/|a|$ 因子 $R$ 的 ROC 大小的变化。因此，$x(t)$ 的时间反转就形成 ROC 的反转，即

$$
x\left(-t\right)\overset{\mathcal{G}}{\leftrightarrow}X\left(-s\right),\qquad\mathrm{R O C}=-R
$$

![图像（物理页 518，第 1 幅）](../Figures/fig-p0518-01.jpg){#fig:p518-1}

**(a)**

![图像（物理页 518，第 2 幅）](../Figures/fig-p0518-02.jpg){#fig:p518-2}

**(b)**

![图像（物理页 518，第 3 幅）](../Figures/fig-p0518-03.jpg){#fig:p518-3}

**(c)**

**图 9.24 时域尺度变换在 ROC 上的影响：**

(a) $ X(s) $的 ROC; (b)a>1, $ (1/|a|)X(s/a) $的 ROC; (c)0>a>-1, $ (1/|a|)X(s/a) $的 ROC

#### 9.5.5 共轭 {#sec:9-5-5}

若

$$
x(t){\overset{\mathcal{L}}{\leftrightarrow}}X(s)\qquad\mathrm{R O C}=R
$$

则

$$
x^{*}(t){\overset{\mathcal{L}}{\leftrightarrow}}X^{*}(s^{*}),\quad\mathrm{R O C}=R
$$

因此

$$
X(s)=X^{*}(s^{*}), 当 \;x(t)\; 为实函数
$$

因此，若 $ x(t) $ 为实函数，如果 $ X(s) $ 有一个极点或零点在 $ s = s_{0} $ (也就是如果 $ X(s) $ 在 $ s = s_{0} $ 无界或为零)，那么 $ X(s) $ 也一定有一个复数共轭的 $ s = s_{0}^{*} $ 的极点或零点。例如，例 9.4 中的实信号 $ x(t) $ 的拉普拉斯变换 $ X(s) $ 就有共轭成对极点 $ s = 1 \pm 3j $ 和零点 $ s = (-5 \pm j\sqrt{71})/2 $。

#### 9.5.6 卷积性质 {#sec:9-5-6}

若

$$
x_{1}(t){\overset{\mathcal{L}}{\leftrightarrow}}X_{1}(s),\qquad\mathrm{R O C}=R_{1}
$$

和

$$
x_{2}(t){\stackrel{\mathcal{X}}{\leftrightarrow}}X_{2}(s),\qquad\mathrm{R O C}=R_{2}
$$

那么

$$
x_{1}(t)*x_{2}(t)\stackrel{\mathcal{L}}{\leftrightarrow}X_{1}(s)X_{2}(s),\quad\mathrm{ROC} \quad \mathrm{ 包括 }\quad R_{1}\cap R_{2}
$$

因此，和9.5.1节的线性性质一样， $ X_{1}(s)X_{2}(s) $的ROC包括 $ X_{1}(s) $和 $ X_{2}(s) $ROC的相交部分，如果在乘积中有零极点相消的话， $ X_{1}(s)X_{2}(s) $的ROC也可以比它们相交的部分大。例如，若

$$
X_{1}(s)=\frac{s+1}{s+2},\qquad\mathcal{R}_{e}\{s\}>-2
$$

和

$$
X_{2}(s)=\frac{s+2}{s+1},\qquad\mathcal{R}_{e}\{s\}>-1
$$

那么 $ X_{1}(s)X_{2}(s)=1 $，它的 ROC 就是整个 s 平面。

正如在第4章中所看到的，傅里叶变换中的卷积性质在线性时不变系统的分析中起着很重要的作用。在9.7节和9.8节，也将利用拉普拉斯变换的卷积性质来分析LTI系统，更具体一些就是分析由线性常系数微分方程所表征的系统。

#### 9.5.7 时域微分 {#sec:9-5-7}

若

$$
x(t){\overset{\mathcal{X}}{\leftrightarrow}}X(s),\qquad\mathrm{R O C}=R
$$

则

$$
\frac{\mathrm{d}x(t)}{\mathrm{d}t}\xleftrightarrow{x}sX(s),\quad\text{ROC包括}R
$$

将(9.56)式的反变换式两边对 t 微分，就可得到这个性质，即设

$$
x(t)=\frac{1}{2\pi\mathrm{j}}\int_{\sigma-\mathrm{j}\infty}^{\sigma+\mathrm{j}\infty}X(s)\mathrm{e}^{\alpha t}\mathrm{d}s
$$

那么就有

$$
\frac{\mathrm{d}x\left(t\right)}{\mathrm{d}t}=\frac{1}{2\pi\mathrm{j}}\int_{\sigma-\mathrm{j}\infty}^{\sigma+\mathrm{j}\infty}s X(s)\mathrm{e}^{s}\mathrm{d}s
$$

可见， $ \mathrm{d}x(t)/\mathrm{d}t $ 就是 $ sX(s) $ 的反变换。 $ sX(s) $ 的 ROC 包括 $ X(s) $ 的 ROC，如果 $ X(s) $ 中有一个 $ s=0 $ 的一阶极点，被乘以 $ s $ 抵消的话，还可以比 $ X(s) $ 的 ROC 大。例如，若 $ x(t)=u(t) $，那么 $ X(s)=1/s $，ROC 是 $ \mathcal{R}\{s\}>0 $，而 $ x(t) $ 的导数是一个单位冲激函数 $ \delta(t) $，它的拉普拉斯变换是 1，而且 ROC 是整个 $ s $ 平面。

#### 9.5.8 s 域微分 {#sec:9-5-8}

将(9.3)式的拉普拉斯变换两边对 s 微分，即

$$
X(s)=\int_{-\infty}^{+\infty}x(t)\mathbf{e}^{-st}\mathrm{d}t
$$

得到

$$
\frac{\mathrm{d}X(s)}{\mathrm{d}s}=\int_{-\infty}^{+\infty}(-\mathrm{~}t\mathrm{~})x(t)\mathrm{e}^{-s}\mathrm{d}t
$$

因此，若

$$
x(t){\overset{\mathcal{L}}{\leftrightarrow}}X(s),\qquad\mathrm{R O C}=R
$$

则

$$
-t x(t){\stackrel{\varphi}{\leftrightarrow}}{\frac{\mathrm{d}X(s)}{\mathrm{d}s}},\quad\mathrm{R O C}=R
$$

下面两个例子用来说明这个性质的应用。

**例 9.14 求下面 $ x(t) $ 的拉普拉斯变换**

$$
x(t)=t\mathrm{e}^{-a t}u(t)
$$

因为

$$
\mathrm{e}^{-a t}u(t)\overset{\mathcal{L}}{\leftrightarrow}\frac{1}{s+a},\qquad\mathcal{R}_{\bullet}|_{S}\rbrace>-a
$$

因此由(9.100)式可得

$$
t\mathbf{e}^{-a d}u(t){\stackrel{\mathcal{L}}{\leftrightarrow}}-\frac{\mathrm{d}}{\mathrm{d}s}\bigg[\frac{1}{s+a}\bigg]=\frac{1}{(s+a)^{2}},\qquad\mathcal{R}_{\bullet}\{s\}|>-a
$$

事实上，反复利用(9.100)式，可得

$$
\frac{t^{2}}{2}\mathrm{e}^{-\alpha t}u\left(t\right)\overset{\underline{{x}}}{\leftrightarrow}\frac{1}{\left(s+a\right)^{3}},\qquad\mathcal{D}_{\bullet}\vert_{s}\vert>-a
$$

或更一般形式为

$$
\frac{t^{n-1}}{(n-1)!}\mathrm{e}^{-a t}u(t)\xrightarrow{x}\frac{1}{(s+a)^{n}},\qquad\mathcal{R}_{\bullet}\{s\}>-a
$$

下一个例子要说明，当将部分分式展开用于求一个具有重阶极点有理函数的反变换时，这个特殊的拉普拉斯变换对是特别有用的。

例 9.15 考虑下面已知拉普拉斯变换 $ X(s) $:

$$
X(s)=\frac{2s^{2}+5s+5}{(s+1)^{2}(s+2)},\qquad\mathcal{R}\{s\}|>-1
$$

将附录中介绍的部分分式展开法应用于 $ X(s) $，可写成

$$
X(s)=\frac{2}{(s+1)^{2}}-\frac{1}{(s+1)}+\frac{3}{s+2},\qquad\mathcal{R}\{s\}>-1
$$

因为 ROC 是在极点 s = -1 和 s = -2 的右边，所以每一项反变换都是一个右边信号，再应用 (9.14) 式和 (9.104) 式，可得反变换为

$$
x(t)=\left[2t\mathrm{e}^{-t}-\mathrm{e}^{-t}+3\mathrm{e}^{-2t}\right]u(t)
$$

#### 9.5.9 时域积分 {#sec:9-5-9}

若

$$
x(t){\overset{\mathcal{L}}{\leftrightarrow}}X(s),\qquad\mathrm{R O C}=R
$$

则

$$
\boxed{\int_{-\infty}^{t}x(\tau)\mathrm{d}\tau\overset{\mathcal{L}}{\longleftrightarrow}\frac{1}{s}X(s)},\mathrm{~\mathrm{R O C} 包括 ~}R\cap\{\mathcal{R}_{e}|s\}>0\}
$$

这个性质是9.5.7节所述微分性质的逆性质，利用9.5.6节的卷积性质可以将它导出，即

$$
\int_{-\infty}^{t}x(\tau)\mathrm{d}\tau=u(t)*x(t)
$$

由例9.1，若a=0，则有

$$
u\left(t\right)\overset{\mathcal{S}}{\leftrightarrow}\frac{1}{s},\qquad\mathcal{R e}\left\{s\right\}>0
$$

根据卷积性质有

$$
u(t)*x(t){\overset{\mathcal{L}}{\leftrightarrow}}\frac{1}{s}X(s)
$$

它的 ROC 应包括 X(s) 的 ROC 和 (9.108) 式 u(t) 拉普拉斯变换 ROC 的相交，这就是 (9.106) 式给出的 ROC 结果。

#### 9.5.10 初值与终值定理 {#sec:9-5-10}

若 $ t<0, x(t)=0 $，并且在 t=0 时， $ x(t) $ 不包含冲激或者高阶奇异函数，在这些特别限制下，就可以直接从拉普拉斯变换式中计算出初值 $ x(0^{+}) $ [也就是 $ x(t) $ 当 t 从正值方向趋于 0 时的值] 和终值，即 $ t \to \infty $ 时的 $ x(t) $ 值。

初值定理

$$
x\left(0^{+}\right)=\lim_{s\rightarrow\infty}s X(s)
$$

终值定理

$$
\lim_{t\to\infty}x(t)=\lim_{s\to0}s X(s)
$$

这些结果的导出留在习题9.53中考虑。

例 9.16 初值与终值定理在验证一个信号的拉普拉斯变换计算结果的正确性上是有用的。例如，考虑例 9.4 中的信号 $ x(t) $，由(9.24)式可见 $ x(0^{+})=2 $，同时利用(9.29)式可求出

$$
\lim_{s\to\infty}sX(s)=\lim_{s\to\infty}\frac{2s^{3}+5s^{2}+12}{s^{3}+4s^{2}+14s+20}=2
$$

这是与(9.110)式的初值定理一致的。

#### 9.5.11 性质列表 {#sec:9-5-11}

表9.1 综合了本节中所得到的全部性质，在9.7节将拉普拉斯变换用于线性时不变系统的分析和表征时，会用到很多这些性质。正如已在几个例子中所说明的，拉普拉斯变换及其ROC的各种性质，都能为一个信号和它的变换提供大量的信息，而这些无论是在表征信号上，还是校核一个计算的结果上都是有用的。在9.7节，9.8节以及本章末的习题中，将给出应用这些性质的其它一些例子。

Table: 表9.1 拉箭拉斯变换性质 {#tbl:9-1}

| 节次 | 性质 | 信号 | 拉普拉斯变换 | ROC |
| --- | --- | --- | --- | --- |
|  |  | $ x(t) $ | $ X(s) $ | R |
| $ x_1(t) $ | $ X_1(s) $ | $ R_1 $ |  |  |
| $ x_2(t) $ | $ X_2(s) $ | $ R_2 $ |  |  |
| 9.5.1 | 线性 | $ ax_1(t) + bx_2(t) $ | $ aX_1(s) + bX_2(s) $ | 至少 $ R_1 \cap R_2 $ |
| 9.5.2 | 时移 | $ x(t - t_0) $ | $ e^{-st}X(s) $ | R |
| 9.5.3 | s 域平移 | $ e^{st}x(t) $ | $ X(s - s_0) $ | R 的平移[即若 $ (s - s_0) $ 在 R 中，则 s 就位于 ROC 中] |
| 9.5.4 | 时域尺度变换 | $ x(at) $ | $ \frac{1}{\|a\|}X\left(\frac{s}{a}\right) $ | R/a (即若 s/a 在 R 中，则 s 就位于 ROC 中) |
| 9.5.5 | 共轭 | $ x^*(t) $ | $ X^*(s^*) $ | R |
| 9.5.6 | 卷积 | $ x_1(t) * x_2(t) $ | $ X_1(s)X_2(s) $ | 至少 $ R_1 \cap R_2 $ |
| 9.5.7 | 时域微分 | $ \frac{d}{dt}xt $ | $ sX(s) $ | 至少 R |
| 9.5.8 | s 域微分 | $ -tx(t) $ | $ \frac{d}{ds}X(s) $ | R |
| 9.5.9 | 时域积分 | $ \int_{-\infty}^{t}x(\tau)d(\tau) $ | $ \frac{1}{s}X(s) $ | 至少 $ R \cap \{R_s\} $ > 0} |

初值和终值定理

若 t<0, $ x(t)=0 $ 且在 t=0 不包括任何冲激或高阶奇异函数，则

$$
x(0^{+})=\operatorname*{l i m}_{s\to\infty}s X(s)
$$

$$
\operatorname*{l i m}_{t\to\infty}x(t)=\operatorname*{l i m}_{t\to0}s X(s)
$$

### 9.6 常用拉普拉斯变换对 {#sec:9-6}

如同在9.3节所指出的，把 $ X(s) $分解成较为简单的一些项的线性组合，拉普拉斯反变换往往是很容易求得的，因为这些简单项的拉普拉斯变换可以直接写出来或者极易求得。表9.2列出了若干常用的拉普拉斯变换对。第1对直接由(9.3)式得到。第2和第6对，由例9.1，分别以 $ a=0 $和 $ a=\alpha $代入就可直接求出。利用微分性质于例9.14可得变换对4。在变换对4的基础上，利用9.5.3的性质可得变换对8。变换对3，5，7和9都是分别在变换对2，4，6和8的基础上，再结合9.5.4节的时域尺度变换性质，以 $ a=-1 $代入而得出的。相类似地，变换对10到16都可以利用表9.1的有关性质，在前面那些变换对的基础上导得（见习题9.55）。

Table: 表9.2 基本函数的拉普拉斯变换 {#tbl:9-2}

| 变换对 | 信号 | 变换 | ROC |
| --- | --- | --- | --- |
| 1 | $ \delta(t) $ | 1 | 全部 s |
| 2 | $ u(t) $ | $ \frac{1}{s} $ | $ \mathcal{R}\{s\}\}>0 $ |
| 3 | $ -u(-t) $ | $ \frac{1}{s} $ | $ \mathcal{R}\{s\}\}<0 $ |
| 4 | $ \frac{t^{n-1}}{(n-1)!}u(t) $ | $ \frac{1}{s^a} $ | $ \mathcal{R}\{s\}\}>0 $ |
| 5 | $ \frac{t^{n-1}}{(n-1)!}u(-t) $ | $ \frac{1}{s^a} $ | $ \mathcal{R}\{s\}\}<0 $ |
| 6 | $ e^{-\alpha}u(t) $ | $ \frac{1}{s+a} $ | $ \mathcal{R}\{s\}\}>-a $ |
| 7 | $ -e^{-\alpha}u(-t) $ | $ \frac{1}{s+a} $ | $ \mathcal{R}\{s\}\}<-a $ |
| 8 | $ \frac{t^{n-1}}{(n-1)!}e^{-\alpha}u(t) $ | $ \frac{1}{(s+a)^n} $ | $ \mathcal{R}\{s\}\}>-a $ |
| 9 | $ -\frac{t^{n-1}}{(n-1)!}e^{-\alpha}u(-t) $ | $ \frac{1}{(s+a)^n} $ | $ \mathcal{R}\{s\}\}<-a $ |
| 10 | $ \delta(t-T) $ | $ e^{-sT} $ | 全部 s |
| 11 | $ [\cos\omega_0 t]u(t) $ | $ \frac{s}{s^2 + \omega_0^2} $ | $ \mathcal{R}\{s\}\}>0 $ |
| 12 | $ [\sin\omega_0 t]u(t) $ | $ \frac{\omega_0}{s^2 + \omega_0^2} $ | $ \mathcal{R}\{s\}\}>0 $ |
| 13 | $ [e^{-\alpha}\cos\omega_0 t]u(t) $ | $ \frac{s + a}{(s + a)^2 + \omega_0^2} $ | $ \mathcal{R}\{s\}\}>-a $ |
| 14 | $ [e^{-\alpha}\sin\omega_0 t]u(t) $ | $ \frac{\omega_0}{(s + a)^2 + \omega_0^2} $ | $ \mathcal{R}\{s\}\}>-a $ |
| 15 | $ u_n(t) = \frac{d^n\delta(t)}{dt^n} $ | $ s^n $ | 全部 s |
| 16 | $ u_{-n}(t) = \underbrace{u(t) \cdots \times u(t)}_{n\times n} $ | $ \frac{1}{s^n} $ | $ \mathcal{R}\{s\}\}>0 $ |

### 9.7 用拉普拉斯变换分析与表征 LTI 系统 {#sec:9-7}

拉普拉斯变换的重要应用之一是对于LTI系统的分析与表征。对于LTI系统，拉普拉斯变换的作用直接来自于卷积性质(9.5.6节)，根据这一性质就可以得到，一个LTI系统输入和输出的拉普拉斯变换是通过乘以系统单位冲激响应的拉普拉斯变换联系起来的，即

$$
Y(s)=H(s)X(s)
$$

式中， $ X(s) $， $ Y(s) $和 $ H(s) $分别是系统输入，输出和单位冲激响应的拉普拉斯变换。(9.112)式是与傅里叶变换场合的(4.56)式相对应的。事实上，当 $ s=j\omega $时，(9.112)式拉普拉斯变换中的每一项都变成相应的傅里叶变换，这样(9.112)式就完全相当于(4.56)式。另外，根据3.2节关于LTI系统对复指数信号响应的讨论，若一个LTI系统的输入是 $ x(t)=e^{st} $，那么其输出就一定是 $ H(s)e^{st} $；也就是说， $ e^{st} $是系统的一个特征函数，而其特征值就等于单位冲激响应的拉普拉斯变换。

当 $ s = j\omega $ 时， $ H(s) $ 就是这个 LTI 系统的频率响应。在拉普拉斯变换的范畴内，一般称 $ H(s) $ 为系统函数或转移函数。LTI 系统的很多性质都与系统函数在 s 平面的特性密切相关。下面将用考查几个重要的系统性质和几类重要系统来说明这一点。

#### 9.7.1 因果性 {#sec:9-7-1}

对于一个因果的LTI系统，其单位冲激响应在t<0时为零，因此是一个右边信号，这样根据9.2节的讨论，可见有

一个因果系统的系统函数的 ROC 是某个右半平面。

应该强调的是，相反的结论未必是成立的。这就如例9.19所说明的，一个是位于最右边极点的右边的ROC并不保证系统是因果的，它只是保证单位冲激响应是右边的。然而，如果 $ H(s) $是有理的，那么，如同例9.17和9.18所表明的，可以只须看一下它的ROC是否是右半平面的，就能确定该系统是否是因果的，从而有

对于一个具有有理系统函数的系统来说，系统的因果性就等效于 ROC 位于最右边极点的右边的右半平面。

**例 9.17 有一系统，其单位冲激响应为**

$$
h(t)=\mathrm{e}^{-t}u(t)
$$

因为 $ t<0,h(t)=0 $ ，所以该系统是因果的。同时它的系统函数由例9.1可得

$$
H(s)=\frac{1}{s+1},\qquad\mathcal{R}\{s\}|>-1
$$

在这种情况下，系统函数是有理的，并且ROC是在最右边极点的右边，这就与具有理系统函数的因果性等效于ROC位于最右边极点的右边的结论相一致。

**例 9.18 有一系统，其单位冲激响应为**

$$
h(t)=\mathrm{e}^{-i t}
$$

因为 $ t<0, h(t)\neq0 $ ，所以该系统是非因果的。同时它的系统函数由例9.7有

$$
H(s)=\frac{-2}{s^{2}-1},\qquad-1<\mathcal{R}\{s\}<+1
$$

因此， $ H(s) $ 是有理的，但 ROC 不在最右边极点的右边，这与系统的非因果性是一致的。

例 9.19 考虑下面系统函数：

$$
H(s)=\frac{e^{s}}{s+1},\qquad\mathcal{R}_{0}|_{s^{i}}>-1
$$

对于该系统，其 ROC 是位于最右边极点的右边，因此单位冲激响应必须是右边的。为了确定它的单位冲激响应，首先利用例9.1的结果

$$
\mathrm{e}^{-t}u(t){\overset{\mathcal{L}}{\leftrightarrow}}\frac{1}{s+1},\qquad\mathcal{R}_{0}\{s\}>-1
$$

接下来，根据9.5.2节的时移性质[(9.87)式]，在(9.115)式中的因子 $ e^{s} $ 可以认为是(9.116)式中时间函数的移位，那么

$$
\mathrm{e}^{-(t+1)}u(t+1){\overset{\mathcal{L}}{\leftrightarrow}}\frac{\mathrm{e}^{s}}{s+1},\qquad\mathcal{R}\{s\}|>-1
$$

所以系统的单位冲激响应是

$$
h(t)=\mathrm{e}^{-(t+1)}u(t+1)
$$

它在 $ -1<t<0 $ 不等于零，所以系统不是因果的。这个例子可以作为一个提示：因果性确实意味着ROC是位于最右边极点的右边，但是相反的结论一般是不成立的，除非系统函数是有理的。

可以用完全相类似的方式来处理有关反因果性的概念。如果系统的单位冲激响应在 $ t>0,h(t)=0 $，就说该系统是反因果的。因为在这种情况下， $ h(t) $是左边信号，由9.2节知道，系统函数 $ H(s) $的ROC就必须是某个左半平面。同样，一般来说其相反的结论是不成立的；也就是说，如果 $ H(s) $的ROC是某个左半平面，那么我们所知道的只是 $ h(t) $是左边的。然而，如果 $ H(s) $是有理的，那么ROC位于最左边极点的左边就等效于系统是反因果的。

#### 9.7.2 稳定性 {#sec:9-7-2}

$ H(s) $的ROC也可以与系统的稳定性联系起来。如同在2.3.7节曾提到的，一个LTI系统的稳定性等效于它的单位冲激响应是绝对可积的，这时单位冲激响应的傅里叶变换收敛。因为一个信号的傅里叶变换就等于拉普拉斯变换沿 $ \mathrm{j}\omega $轴求值，所以就有

当且仅当系统函数 $ H(s) $ 的 ROC 包括 $ j\omega $ 轴 [即： $ \mathcal{R}(s)=0 $ ] 时，一个 LTI 系统就是稳定的。

**例 9.20 考虑一 LTI 系统，其系统函数为**

$$
H(s)=\frac{s-1}{(s+1)(s-2)}
$$

因为没有给出 ROC，那么根据 9.2 节的讨论知道，存在着几种不同的 ROC，结果就会有几种不同的单位冲激响应与 (9.119) 式给出的 $ H(s) $ 代数表示式相联系。然而，如果有关于系统的因果性或稳定性方面的信息，那么适当的 ROC 还是能被确定。例如，若系统已知是因果的，那么 ROC 一定为图 9.25(a) 所示，这时的单位冲激响应就是

$$
h(t)=\left(\frac{2}{3}\mathrm{e}^{-t}+\frac{1}{3}\mathrm{e}^{2t}\right)u(t)
$$

注意，这种 ROC 的选择并未包括 $ j\omega $ 轴，因此对应的系统是不稳定的（只要看看 $ h(t) $ 不是绝对可积的就能得出）。另一方面，若系统已知是稳定的，那么 ROC 就如图 9.25(b) 所示，相应的单位冲激响应是

$$
h(t)=\frac{2}{3}\mathrm{e}^{-t}u(t)-\frac{1}{3}\mathrm{e}^{2t}u(-t)
$$

这是绝对可积的。最后，ROC为图9.25(c)所示，这时的单位冲激响应为

$$
h(t)=-\left(\frac{2}{3}\mathrm{e}^{-t}+\frac{1}{3}\mathrm{e}^{2t}\right)u(-t)
$$

系统是反因果的，而且是不稳定的。

![图像（物理页 526，第 1 幅）](../Figures/fig-p0526-01.jpg){#fig:p526-1}

**(a)**

**(c)**

**图 9.25 例9.20系统函数(极点为s=-1和s=2，零点在s=1)的几种可能ROC; (a)因果不稳定系统；(b)非因果稳定系统；(c)反因果不稳定系统**

当然，一个系统是稳定的（或不稳定），而有一个非有理的系统函数，这完全是可能的。例如，(9.115)式的系统函数不是有理的，而它的单位冲激响应(9.118)式是绝对可积的，这就表明系统是稳定的。然而，对于具有有理系统函数的系统，其稳定性是很容易用系统的极

点来说明的。例如，对于图9.25的零极点图，稳定性就对应于ROC的选择要在两个极点之间，以使得jω轴位于ROC内。

对于一种特别而重要的系统，稳定性可以很简单地用极点的位置来表征。具体一些就是，考虑一个因果 LTI 系统，具有有理系统函数 $ H(s) $，因为系统是因果的，ROC 就在最右边极点的右边，因此，这个系统要是稳定的话（即，ROC 包括 $ j\omega $ 轴）， $ H(s) $ 的最右边的极点必须位于 $ j\omega $ 轴的左边，即

当且仅当 $ H(s) $ 的全部极点都位于 s 平面的左半平面时，也即全部极点都有负的实部时，一个具有有理系统函数 $ H(s) $ 的因果系统才是稳定的。

例 9.21 再次考虑例 9.17 的因果系统，(9.113)式的单位冲激响应是绝对可积的，因此该系统是稳定的。与此相一致的是，由(9.114)式给出的 $ H(s) $，其极点在 s = -1，它在 s 平面的左半平面。与此相反，单位冲激响应为

$$
h(t)=\mathrm{e}^{2t}u(t)
$$

的因果系统是不稳定的，因为 $ h(t) $不是绝对可积的。同时，在这个情况下

$$
H(s)=\frac{1}{s-2},\qquad\mathcal{R}\{s\}>2
$$

系统有一个极点在 s=2，它位于 s 平面的右半平面。

例9.22 考虑曾在9.4.2节和6.5.2节讨论过的因果二阶系统，单位冲激响应和系统函数分别是

$$
h(t)=M[\mathrm{e}^{c_{1}t}-\mathrm{e}^{c_{2}t}]u(t)
$$

和

$$
\begin{aligned}{H(s)}&{{}=\frac{\omega_{n}^{2}}{s^{2}+2\zeta\omega_{n}s+\omega_{n}^{2}}}\\ {}&{{}=\frac{\omega_{n}^{2}}{(s-c_{1})(s-c_{2})}}\\ \end{aligned}
$$

式中

$$
c_{1}=-\zeta\omega_{n}+\omega_{n}\sqrt{\zeta^{2}-1}
$$

$$
c_{2}=-\zeta\omega_{n}-\omega_{n}\sqrt{\zeta^{2}-1}
$$

![图像（物理页 527，第 1 幅）](../Figures/fig-p0527-01.jpg){#fig:p527-1}

$$
M=\frac{\omega_{n}}{2\sqrt{\zeta^{2}-1}}
$$

**图 9.26 $ \zeta<0 $ 时，一个因果二阶系统的极点位置和 ROC**

在图9.19中，已经标出了对 $ \zeta>0 $时的

极点位置。在图9.26中标明的是 $ \zeta<0 $时的极点位置。从后面这个图以及(9.124)式和(9.125)式都很明显地看出，对于 $ \zeta<0 $，两个极点都有正的实部，结果对于 $ \zeta<0 $，这个因果的二阶系统不可能是稳定的。这个在(9.121)式中也是显然的，因为 $ \mathcal{R}_{0}\{c_{1}\}>0 $和 $ \mathcal{R}_{0}\{c_{2}\}>0 $，每一项都随t的增

加而指数增长，因此 $ h(t) $不可能是绝对可积的。

#### 9.7.3 由线性常系数微分方程表征的 LTI 系统 {#sec:9-7-3}

在 4.7 节已经讨论过利用傅里叶变换来得到一个由线性常系数微分方程表征的 LTI 系统的频率响应，而用不着首先解出单位冲激响应或时域解。用完全相类似的方式，拉普拉斯变换的性质也能用来直接求得一个由线性常系统微分方程所表征的系统的系统函数。在下面的例子中用来说明这一过程。

例 9.23 考虑一 LTI 系统，其输入 $ x(t) $ 和输出 $ y(t) $ 满足如下线性常系数微分方程：

$$
\frac{\mathrm{d}y(t)}{\mathrm{d}t}+3y(t)=x(t)
$$

在(9.126)式两边应用拉普拉斯变换，并分别用9.5.1节的线性性质和9.5.7节的微分性质，可得代数方程

$$
s Y(s)+3Y(s)=X(s)
$$

因为由(9.112)式，系统函数是

$$
H(s)=\frac{Y(s)}{X(s)}
$$

可得该系统的系统函数是

$$
H(s)=\frac{1}{s+3}
$$

这就给出了系统函数的代数表示式，但没有收敛域。事实上，正如在2.4节所讨论的，微分方程本身并不能完全表征这个LTI系统，可以有不同的单位冲激响应都与这个微分方程相吻合。如果，除了这个微分方程之外，还知道系统是因果的，那么ROC就可以推断出是在最右边极点的右边，在这个例子中就对应于 $ \mathcal{R}_{s}\} > -3 $；如果已知系统是反因果的，那么ROC就是 $ \mathcal{R}_{s}\} < -3 $。在因果的情况下，相应的单位冲激响应是

$$
h(t)=\mathrm{e}^{-3t}u(t)
$$

而在反因果的情况下则是

$$
h(t)=-\mathrm{e}^{-3t}u(-t)
$$

在例9.23中由微分方程得到 $ H(s) $的过程可以应用到更一般的情况。考虑如下形式的线性常系数微分方程：

$$
\sum_{k=0}^{N}a_{k}\frac{\mathrm{d}^{k}y(t)}{\mathrm{d}t^{k}}=\sum_{k=0}^{M}b_{k}\frac{\mathrm{d}^{k}x(t)}{\mathrm{d}t^{k}}
$$

在上式两边进行拉普拉斯变换，并反复应用线性和微分性质，可得

$$
\big(\sum_{k=0}^{N}a_{k}s^{k}\big)Y(s)\;=\;\big(\sum_{k=0}^{M}b_{k}s^{k}\big)X(s)
$$

或者

$$
H(s)\;=\;{\frac{\big|\sum_{k=0}^{M}b_{k}s^{k}\big|}{\big|\sum_{k=0}^{N}a_{k}s^{k}\big|}}
$$

因此，一个由微分方程表征的系统，其系统函数总是有理的，它的零点就是下列方程的解：

$$
\sum_{k=0}^{M}b_{k}s^{k}=0
$$

而它的极点就是如下方程的解：

$$
\sum_{k=0}^{N}a_{k}s^{k}=0
$$

和前面的讨论一样，(9.133)式并没有包括 $ H(s) $ 收敛域的说明，因为该线性常系数微分方程本身没有限制收敛域。然而，如果给出系统有关稳定性或因果性的附加说明，收敛域就可以被推演出来。例如，如果在系统上强加上初始松弛的条件，它就是因果的，那么 ROC 就一定是位于最右边极点的右边。

例 9.24 一个 RLC 电路，若其电容器上的电压和电感线圈中的电流最初都是零，就构成了一个可用线性常系数微分方程描述的 LTI 系统。现考虑图 9.27 的串联 RLC 电路，设跨于电压源的电压是输入信号 x(t)，跨于电容器上的电压是输出信号 y(t)。令在电阻、电感和电容器上的电压之和等于电源电压，就得

![图像（物理页 529，第 1 幅）](../Figures/fig-p0529-01.jpg){#fig:p529-1}

$$
R C\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+L C\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}+y\left(t\right)=x\left(t\right)
$$

**图 9.27 串联 RLC 电路**

应用(9.133)式，可得

$$
H(s)=\frac{1/LC}{s^{2}+(R/L)s+(1/LC)}
$$

正如在习题9.64中所指出，如果R,L和C的值全是正的，该系统函数的极点就全具有负的实部，因此该系统一定是稳定的。

#### 9.7.4 系统特性与系统函数的关系举例 {#sec:9-7-4}

已经看到，像因果性和稳定性这些系统性质都能直接与系统函数及其特性联系起来。事实上，已经给出的拉普拉斯变换的每一个性质都能以这种方式用于将系统特性与系统函数联系起来。这一节将用几个例子来说明这一点。

**例 9.25 假设已知，若一个 LTI 系统的输入是**

$$
x(t)=\mathrm{e}^{-3t}u(t)
$$

那么其输出就是

$$
y(t)=[\mathrm{e}^{-t}-\mathrm{e}^{-2t}]u(t)
$$

现在要证明，根据这些认识就能确定该系统的系统函数，并且由此还可立即推断出系统的其它性质。

将 $ x(t) $ 和 $ y(t) $ 分别取拉普拉斯变换得

$$
X(s)=\frac{1}{s+3},\qquad\mathcal{R}_{\bullet}\{s\}|>-3
$$

和

$$
Y(s)=\frac{1}{(s+1)(s+2)},\qquad\mathcal{R}\{s\}>-1
$$

由(9.112)式可以得到

$$
H(s)=\frac{Y(s)}{X(s)}=\frac{s+3}{(s+1)(s+2)}=\frac{s+3}{s^{2}+3s+2}
$$

再者，还可以确定系统函数的 ROC。由 9.5.6 节的卷积性质知道， $ Y(s) $ 的 ROC 至少必须包括 $ X(s) $ 和 $ H(s) $ 的 ROC 的相交部分。检查一下 $ H(s) $ ROC 的三种可能情况（即：极点 $ s = -2 $ 的左边，极点 -2 和极点 -1 之间，以及极点 $ s = -1 $ 的右边），可见只有 $ \mathcal{R}\{s\} > -1 $ 一种选择才能与 $ X(s) $ 和 $ Y(s) $ 的 ROC 相符合。因为这个 ROC 就是 $ H(s) $ 的最右边极点的右边，因此可得 $ H(s) $ 是因果的。又因为 $ H(s) $ 的两个极点都有负的实部，所以系统又是稳定的。再者，根据 (9.131) 式和 (9.133) 式之间的关系，还能给出下列微分方程，与初始松弛条件一起

$$
\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}+3\frac{\mathrm{d}y(t)}{\mathrm{d}t}+2y(t)=\frac{\mathrm{d}x(t)}{\mathrm{d}t}+3x(t)
$$

来表征这个系统。

例 9.26 假定关于某个 LTI 系统已知下列信息：

1. 系统是因果的。

2. 系统函数是有理的，且仅有两个极点在 s = -2 和 s = 4。

3. 若 $ x(t)=1 $，则 $ y(t)=0 $。

4. 单位冲激响应在 $ t=0^{+} $ 时的值是 4。

根据以上信息，要想确定该系统的系统函数。

根据1和2可知，系统是不稳定的（因为系统是因果的，而又有一个实部为正的极点在s=4），并且系统函数具有如下形式：

$$
H(s)=\frac{p(s)}{(s+2)(s-4)}=\frac{p(s)}{s^{2}-2s-8}
$$

式中 $ p(s) $ 是一个 s 的多项式。由于对输入 $ x(t)=1=e^{0\cdot t} $ 的响应 $ y(t) $ 必须等于 $ H(0)\cdot e^{0\cdot t}=H(0) $，因此由 3 可得 $ p(0)=0 $，也就是说 $ p(s) $ 必定有一个根在 s=0，于是 $ p(s) $ 就应具有

$$
p(s)=s q(s)
$$

式中 $ q(s) $ 是另一个 s 多项式。

最后，根据4和9.5.10节中的初值定值，可知

$$
\lim_{s\to\infty}s H(s)=\lim_{s\to\infty}\frac{s^{2}q(s)}{s^{2}-2s-8}=4
$$

当 $ s \to \infty $ 时， $ sH(s) $ 的分子和分母中 s 的最高次项起支配作用，从而在求 (9.138) 式中是仅仅起作用的项；再者，若分子的阶比分母的阶高，那么这个极限一定发散，因此对于这个极限要能得到一个有限的非零值，唯有在 $ sH(s) $ 是分子分母同阶次的情况方有可能。现在已经知道分母阶次为 2，因此要使 (9.138) 式能成立， $ q(s) $ 必须是一个常数，即 $ q(s) = K $。这个常数可以按如下求出：

$$
\lim_{s\to\infty}\frac{K s^{2}}{s^{2}-2s-8}=\lim_{s\to\infty}\frac{K s^{2}}{s^{2}}=K
$$

令(9.138)式和(9.139)式相等，可见 K=4，因此

$$
H(s)=\frac{4s}{(s+2)(s-4)}
$$

例 9.27 考虑一个稳定而因果的系统，其单位冲激响应为 $ h(t) $，系统函数为 $ H(s) $。假定 $ H(s) $ 是有理的，有一个极点在 s = -2，原点没有零点，其余的极点和零点位置都不知道。对于下列每一种说法判

断：是否能肯定地说是对的，是否能肯定地说是错的，或者说由于条件不充分而无法确认它的真

实性：

(a) $ \mathcal{F}\{h(t)e^{3t}\} $收敛。

(b) $ \int_{-\infty}^{+\infty} h(t) dt = 0 $.

(c) $ th(t) $是一个因果而稳定系统的单位冲激响应。

(d) $ dh(t)/dt $ 在它的拉普拉斯变换中至少有一个极点。

(e) $ h(t) $ 是有限持续期的。

(f) $ H(s)=H(-s) $

(g) $ \lim_{s\to\infty}H(s)=2 $。

(a) 是错的。因为 $ \mathcal{F}(h(t)\mathrm{e}^{3t}) $ 相应于 $ h(t) $ 的拉普拉斯变换在 s = -3 ⑪ 的值，如果这个值收敛，那就意味着 s = -3 是在收敛域 ROC 内。但是一个因果而稳定的系统它的 ROC 总是在它的全部极点的右边，可是 s = -3 不在极点 s = -2 的右边。

(b)也是错的。因为这等于说 $ H(0)=0 $，可是已知 $ H(s) $在原点没有零点。

(c)的说法是对的。按表9.1所列的在9.5.8节得到的性质， $ th(t) $的拉普拉斯变换与 $ H(s) $有相同的ROC，而 $ H(s) $的ROC包括 $ \mathrm{j}\omega $轴，因此对应的系统是稳定的。同时，对于 $ t<0,h(t)=0 $，这意味着 $ t<0 $，也有 $ th(t)=0 $，因此由 $ th(t) $代表的是一个因果系统的单位冲激响应。

(d)也是对的。因为根据表9.1， $ \mathrm{d}h(t)/\mathrm{d}t $ 的拉普拉斯变换为 $ sH(s) $，而乘一个 s 并没有消去在 s = -2 的极点。

(e)是错的。如果 $ h(t) $是有限持续期的话，它的拉普拉斯变换的ROC就必须是整个s平面，然而 $ H(s) $在s=-2已经有极点。

(i)也是错的。倘若这是对的，那么，因为 $ H(s) $在s=-2有一个极点，那就也必须在s=2有一个极点；而对于一个因果而稳定的系统，其全部极点都一定位于s平面的左半面，这是相矛盾的。

(g)的说法的真假由给出的条件无法肯定。因为这种情况要求 $ H(s) $分子分母同阶次，但是缺乏足够的条件来判断 $ H(s) $是否属于这种情况。

#### 9.7.5 巴特沃兹滤波器 {#sec:9-7-5}

在例6.3中曾简要介绍过称之为巴特沃兹滤波器一类广泛应用的LTI系统。这类滤波器有几个性质，其中包括这类滤波器中的每一种频率响应的模特性，在实际实现中颇具吸引力。作为拉普拉斯变换应用的进一步说明，这一节将用拉普拉斯变换技术从频率响应模特性的要求中来确定巴特沃兹滤波器的系统函数。

一个N阶低通巴特沃兹滤波器频率响应的模平方是

$$
1~B\left(\mathrm{j}\omega\right)~\mathrm{1}^{2}=\frac{1}{1+\left(\mathrm{j}\omega/\mathrm{j}\omega_{c}\right)^{2N}}
$$

式中 N 是滤波器的阶。从(9.140)式要确定系统函数 $ B(s) $，该系统函数可给出 $ |B(j\omega)|^{2} $ 的特性。首先按定义

$$
\mid B(\mathrm{j}\omega)\mid^{2}=B(\mathrm{j}\omega)B^{*}(\mathrm{j}\omega)
$$

如果将该巴特沃兹滤波器的单位冲激响应限制为实值函数，那么由傅里叶变换的共轭对称性质，就有

$$
B^{*}(\mathrm{j}\omega)=B(-\mathrm{j}\omega)
$$

这样

$$
B(\mathrm{j}\omega)B(-\mathrm{j}\omega)=\frac{1}{1+\left(\mathrm{j}\omega/\mathrm{j}\omega_{c}\right)^{2N}}
$$

注意到 $ B(s) \big|_{s=j\omega} = B(j\omega) $，由(9.143)式就有

$$
B(s)B(-s)=\frac{1}{1+(s/\mathrm{j}\omega_{c})^{2N}}
$$

这个分母多项式的根就是 $ B(s)B(-s) $ 的极点，这些极点应位于

$$
s=(-1)^{1/2N}(\mathrm{j}\omega_{\mathrm{c}})
$$

(9.145)式对如下 $ s=s_{p} $都满足

$$
\mathrm{~f~s}_{p}\mid=\omega_{c}
$$

$$
\begin{aligned} 令 s_{p}&=\frac{\pi(2k+1)}{2N}+\frac{\pi}{2},\quad&k& 为整数 \end{aligned}
$$

也即

$$
s_{p}=\omega_{c}\mathrm{e x p}\Big(\mathrm{j}\Big[\frac{\pi(2k+1)}{2N}+\pi/2\Big]\Big)
$$

在图9.28中画出N=1,2,3和6时， $ B(s)B(-s) $的极点位置。关于 $ B(s)B(-s) $的极点，一般可以给出如下几点判断：

![图像（物理页 532，第 1 幅）](../Figures/fig-p0532-01.jpg){#fig:p532-1}

![图像（物理页 532，第 2 幅）](../Figures/fig-p0532-02.jpg){#fig:p532-2}

![图像（物理页 532，第 3 幅）](../Figures/fig-p0532-03.jpg){#fig:p532-3}

![图像（物理页 532，第 4 幅）](../Figures/fig-p0532-04.jpg){#fig:p532-4}

**图 9.28 N=1, 2, 3 和 6 时， $ B(s)B(-s) $ 的极点位置**

1. 在 s 平面内，半径为 $ \omega_{c} $ 的圆上，有 2N 个极点在角度上成等分割配置。

2. 极点永远不会位于 $ j\omega $ 轴上，而且当 N 为奇数时，在 $ \sigma $ 轴上有极点，N 为偶数时则没有。

3. 相邻极点之间的角度差是 $ \pi/N $ 弧度。

在已知 $ B(s)B(-s) $ 极点的情况下，为了确定 $ B(s) $ 的极点，可以观察到， $ B(s)B(-s) $ 的极点总是成对出现的，即如果有一个极点是在 $ s=s_{p} $，那么就也有一个极点在 $ s=-s_{p} $。因此，为了构成 $ B(s) $ 的极点，可以从每对极点当中选取一个。若将系统限为稳定和因果的，那么与 $ B(s) $ 有关的极点就应该是位于该圆上沿左半面半圆上的极点。除了一个常数因子外，这些极点位置就给出了 $ B(s) $ 的性质。然而，从 (9.144) 式看到 $ B^{2}(s)|_{s=0}=1 $，或者等效地说，按 (9.140) 式，常数因子选择成使频率响应的模平方在 $ \omega=0 $ 时为单位增益。

![图像（物理页 533，第 1 幅）](../Figures/fig-p0533-01.jpg){#fig:p533-1}

![图像（物理页 533，第 2 幅）](../Figures/fig-p0533-02.jpg){#fig:p533-2}

**图 9.29 N=1, 2 和 3 时， $ B(s) $ 的极点位置**

为了说明 $ B(s) $ 的确定，现考虑 N=1, N=2 和 N=3 时的情况。根据(9.148)式已在图9.28中画出了 $ B(s)B(-s) $ 的极点，对于所给三种 N 值的情况，在图9.29中指出了与 $ B(s) $ 有关的极点。这些相应的转移函数就是

$$
N=1;\quad B(s)=\frac{\omega_{c}}{s+\omega_{c}}
$$

$$
N=2\colon\qquad B(s)=\frac{\omega_{c}^{2}}{(s+\omega_{c}\mathrm{e}^{\mathrm{j}(\pi/4)})(s+\omega_{c}\mathrm{e}^{-\mathrm{j}(\pi/4)})}=\frac{\omega_{c}^{2}}{s^{2}+\sqrt{2}\omega_{c}s+\omega_{c}^{2}}
$$

$$
\begin{aligned}{B(s)}&{{}=\frac{\omega_{c}^{3}}{(s+\omega_{c})(s+\omega_{c}\mathrm{e}^{\mathrm{j}(\pi/3)})(s+\omega_{c}\mathrm{e}^{-\mathrm{j}(\pi/3)})}}\\ {}&{{}=\frac{\omega_{c}^{3}}{(s^{2}+\omega_{c})(s^{2}+\omega_{c}s+\omega_{c}^{2})}=\frac{\omega_{c}^{3}}{s^{3}+2\omega_{c}s^{2}+2\omega_{c}^{2}s+\omega_{c}^{3}}}\\ \end{aligned}
$$

根据9.7.3节的讨论，由 $ B(s) $可以确定与其相关的线性常系数微分方程。对应以上三种N值，相应的微分方程就是

$$
N=1;\quad\frac{\mathrm{d}y(t)}{\mathrm{d}t}+\omega_{c}y(t)=\omega_{c}x(t)
$$

$$
\mathrm{N}=2:\quad\frac{\mathrm{d}^{2}\mathbf{y}\left(t\right)}{\mathrm{d}t^{2}}+\sqrt{2}\omega_{c}\ \frac{\mathrm{d}\mathbf{y}\left(t\right)}{\mathrm{d}t}+\omega_{c}^{2}\mathbf{y}\left(t\right)=\omega_{c}^{2}x\left(t\right)
$$

$$
\mathrm{N}=3;\quad\frac{\mathrm{d}^{3}\mathrm{y}\left(t\right)}{\mathrm{d}t^{3}}+2\omega_{c}\frac{\mathrm{d}^{2}\mathrm{y}\left(t\right)}{\mathrm{d}t^{2}}+2\omega_{c}^{2}\frac{\mathrm{d}\mathrm{y}\left(t\right)}{\mathrm{d}t}+\omega_{c}^{3}\mathrm{y}\left(t\right)=\omega_{c}^{3}r\left(t\right)
$$

### 9.8 系统函数的代数属性与方框图表示 {#sec:9-8}

利用拉普拉斯变换可以将微分、卷积、时移等这些时域中的运算用代数运算来代替。已经看到了这样做在分析LTI系统中的很多好处。在这一节将要看看系统函数代数属性的另一个重要应用，即在分析LTI系统的互联，以及用基本系统的构造单元的互联来综合出复杂系统中的应用。

#### 9.8.1 LTI 系统互联的系统函数 {#sec:9-8-1}

考虑两个系统的并联，如图9.30(a)所示。总系统的单位冲激响应是

$$
h(t)=h_{1}(t)+h_{2}(t)\left(9.155\right)
$$

由拉普拉斯变换的线性性质，有

$$
H(s)=H_{1}(s)+H_{2}(s)
$$

同理，两个系统的级联，如图9.30(b)所示，其单位冲激响应为

$$
h(t)=h_{1}(t)*h_{2}(t)\left(9.157\right)
$$

$$
H(s)=H_{1}(s)H_{2}(s)
$$

和系统函数是

通过代数运算利用拉普拉斯变换在表示线性系统的互联中可以扩展到远比图9.30这种简单的并联和级联更为复杂的互联中去。为此，考虑一下图9.31所指出的两个系统的反馈互联。第11章

![图像（物理页 534，第 1 幅）](../Figures/fig-p0534-01.jpg){#fig:p534-1}

**(a)**

![图像（物理页 534，第 2 幅）](../Figures/fig-p0534-02.jpg){#fig:p534-2}

**(b)**

**图 9.30 (a) 两个 LTI 系统的并联；**

**(b)两个LTI系统的级联**

要详细讨论这类互联系统的设计、应用和分析。尽管在时域中分析这类系统不是特别简单，但是确定由输入 $ x(t) $到输出 $ y(t) $的总系统函数还是一个直接的代数运算。具体地说，由图

9.31 有

$$
Y(s)=H_{1}(s)E(s)
$$

$$
E(s)=X(s)-Z(s)
$$

和

![图像（物理页 535，第 1 幅）](../Figures/fig-p0535-01.jpg){#fig:p535-1}

$$
Z(s)=H_{2}(s)Y(s)
$$

**图 9.31 两个 LTI 系统的反馈互联**

由此可得

$$
\mathrm{Y}(s)=\mathrm{H}_{1}(s)\big[\mathrm{X}(s)-\mathrm{H}_{2}(s)\mathrm{Y}(s)\big]
$$

或者

$$
\frac{Y(s)}{X(s)}=H(s)=\frac{H_{1}(s)}{1+H_{1}(s)H_{2}(s)}
$$

#### 9.8.2 由微分方程和有理系统函数描述的因果LTI系统的方框图表示 {#sec:9-8-2}

在2.4.3节曾说明过，利用相加，乘以系数和积分这些基本运算，将由一阶微分方程描述的LTI系统用方框图来表示。这三种运算也能用来构造更高阶系统的方框图，本节将用几个例子来给予说明。

例 9.28 考虑一因果 LTI 系统，其系统函数 $ H(s) $ 为

$$
H(s)\simeq\frac{1}{s+3}
$$

由9.7.3节知道，这个系统也能用下列微分方程来描述：

$$
\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+3y\left(t\right)=x\left(t\right)
$$

具有初始松弛条件。在2.4.3节曾构造出一个方框图表示如图2.32所示。另一种等效的方框图（相应于图2.32中的a=3和b=1）如图9.32（a）所示。图中1/s是一个单位冲激响应为 $ u(t) $的系统的系统函数，也就是一个积分器的系统函数。在图9.32（a）的反馈回路中的系统函数-3就相应于乘以系数-3。这个方框图中所涉及的反馈回路很像上一小节所考虑，并画在图9.31的反馈回路，唯一的差别是输入到相加器中的这两个信号在图9.32（a）中是相

**(a)**

![图像（物理页 535，第 2 幅）](../Figures/fig-p0535-02.jpg){#fig:p535-2}

![图像（物理页 535，第 3 幅）](../Figures/fig-p0535-03.jpg){#fig:p535-3}

**图 9.32 (a) 例 9.28 的因果 LTI 系统的方框图表示; (b) 等效方框图表示**

加，而不是在图9.31中是相减。然而，若在反馈回路中改变相乘系数的符号，所得出的图9.32(b)就与图9.31完全一样了。这样可用(9.163)式证明出

$$
H(s)=\frac{1/s}{1+3/s}=\frac{1}{s+3}
$$

例 9.29 现在考虑一因果 LTI 系统，其系统函数 $ H(s) $ 为

$$
H(s)=\frac{s+2}{s+3}=\left(\frac{1}{s+3}\right)(s+2)
$$

![图像（物理页 536，第 1 幅）](../Figures/fig-p0536-01.jpg){#fig:p536-1}

**(a)**

![图像（物理页 536，第 2 幅）](../Figures/fig-p0536-02.jpg){#fig:p536-2}

**(b)**

**图 9.33 (a) 例 9.29 的系统方框图表示；(b) 等效方框图表示**

由(9.164)式可以想到，这个系统可以看成是一个系统函数为 $ 1/(s+3) $ 的系统与系统函数为 $ (s+2) $ 的系统的级联结果。这就如图9.33(a) 所示，图中已经用了图9.32(a) 的方框图来代表 $ 1/(s+3) $。

对于(9.164)式的系统，还有可能得到另一种方框图表示。利用拉普拉斯变换的线性和微分性质可知，图9.33(a)中 $ y(t) $和 $ z(t) $是由下列方程关联起来的：

$$
y(t)=\frac{\mathrm{d}z(t)}{\mathrm{d}t}+2z(t)
$$

然而，输入至积分器的 $ e(t) $就是输出 $ z(t) $的导数，所以

$$
y(t)=e(t)+2z(t)
$$

这就直接导出另一种方框图表示，如图9.33(b)所示。注意，因为

$$
y(t)=\frac{\mathrm{d}z(t)}{\mathrm{d}t}+2z(t)
$$

方框图图9.33(a)要求 $ z(t) $的微分，而与此对照，图9.33(b)并不涉及到任何信号的直接微分。

例 9.30 接下来考虑一因果二阶系统，其系统函数为

$$
H(s)=\frac{1}{(s+1)(s+2)}=\frac{1}{s^{2}+3s+2}
$$

![图像（物理页 537，第 1 幅）](../Figures/fig-p0537-01.jpg){#fig:p537-1}

**(a)**

**(b)**

**(c)**

**图 9.34 例 9.30 系统的方框图表示: (a) 直接型; (b) 级联型; (c) 并联型**

这个系统的输入 $ x(t) $ 和输出 $ y(t) $ 满足下面微分方程：

$$
\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}+3\frac{\mathrm{d}y(t)}{\mathrm{d}t}+2y(t)=x(t)
$$

采用上面例子的类似想法，可以得出这个系统的方框图表示如图9.34(a)所示。因为，积分器的输入就是积分器输出的导数，所以方框图中各信号关联如下：

$$
f(t)=\frac{\mathrm{d}y(t)}{\mathrm{d}t}
$$

$$
e(t)=\frac{\mathrm{d}f(t)}{\mathrm{d}t}=\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}
$$

同时，将(9.166)式重写成

$$
\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}=-\mathrm{3}\frac{\mathrm{d}y(t)}{\mathrm{d}t}-2y(t)+x(t)
$$

或者

$$
e(t)=-3f(t)-2y(t)+x(t)
$$

这是与图9.34(a)所代表的完全相同的。

因为在这个图上所出现的系数可以直接从系统函数中的系数，或等效为微分方程中的系数确认出来，所以称这种方框图为直接型表示。稍许对系统函数作些变化，可以得到实际中很重要的其

它方框图表示。这就是，(9.165)式的 $ H(s) $可重写成

$$
H(s)=\left(\frac{1}{s+1}\right)\left(\frac{1}{s+2}\right)
$$

这就使人想到能将该系统表示成两个一阶系统的级联。这种级联型表示如图9.34(b)所示。另外，将 $ H(s) $作部分分式展开，可得

$$
H(s)=\frac{1}{s+1}-\frac{1}{s+2}
$$

这就导致并联型表示，如图9.34(c)所示。

**例 9.31 作为最后一个例子，考虑如下系统函数：**

$$
H(s)\;=\frac{2s^{2}+4s-6}{s^{2}+3as+2}
$$

再次利用系统函数的代数属性，可将 $ H(s) $ 写成几种不同的形式，其中每一种都有一种方框图表示。特别是，能将 $ H(s) $ 写成

$$
H(s)=\left(\frac{1}{s^{2}+3s+2}\right)(2s^{2}+4s-6)
$$

这就是 $ H(s) $ 可看成是图 9.34(a) 的系统与系统函数为 $ (2s^{2} + 4s - 6) $ 的系统的级联。完全就像在例 9.29 中所做的那样，可以用“抽头”信号的办法把出现在第一个系统积分器输入端的信号抽出来，以提取这第二个系统所要求的导数。有关这一详细过程将在习题 9.36 中讨论，而对于所得的直接型方框图表示则如图 9.35 所示。再一次看到，在直接型表示中，方框图中所出现的系数可以凭直观直接由系统函数 (9.167) 式中的系数来确定。

![图像（物理页 538，第 1 幅）](../Figures/fig-p0538-01.jpg){#fig:p538-1}

**图 9.35 例 9.31 系统的直接型表示**

另外，还能将 $ H(s) $写成

$$
H(s)=\left(\frac{2(s-1)}{s+2}\right)\left(\frac{s+3}{s+1}\right)
$$

或者

$$
H(s)=2+\frac{6}{s+2}-\frac{8}{s+1}
$$

其中的第一个是一种级联型表示，而第二个则是一种并联型表示。这些都将在习题9.36中讨论。

对于由微分方程和有理系统函数描述的因果LTI系统构造方框图表示的方法都可以用于高阶的系统。另外，往往在如何构成上有很大的灵活性。例如，若将(9.168)式中的分子颠倒一下次序，就可写成

$$
H(s)\simeq\left(\frac{s+3}{s+2}\right)\left(\frac{2(s-1)}{s+2}\right)
$$

这又是一种不同的级联型表示。同样，正如在习题9.38中所说明的，一个四阶系统函数可以写成两个二阶系统函数的乘积，而其中每个二阶系统函数又有几种不同的表示方式（譬如，直接型、级联型或并联型）；并且还能写成低阶项的和，而每个低阶项又有几种不同的表示。这样一来，简单的低阶系统就可以作为基本的构造单元，用来实现更加复杂的高阶系统。

### 9.9 单边拉普拉斯变换 {#sec:9-9}

本章前面各节所讨论的拉普拉斯变换一般称为双边拉普拉斯变换。稍许有些不同的另一种拉普拉斯变换形式称为单边拉普拉斯变换，将在这一节给予介绍和讨论。单边拉普拉斯变换在分析具有非零初始条件的（也即系统最初不是松弛的），由线性常系数微分方程所描述的因果系统中也有很大的价值。

一个连续时间信号 $ x(t) $ 的单边拉普拉斯变换 $ \mathcal{X}(s) $ 定义为

$$
\mathcal{X}(s)\triangleq\int_{0^{-}}^{\infty}x(t)\mathrm{e}^{-st}\mathrm{d}t
$$

这里，积分的下式取为 $ 0^{-} $，以表明在积分区间内包括了集中于 t=0 的任何冲激或高阶奇异函数。对于一个信号和它的单边拉普拉斯变换再次采用一个方便的简化符号为

$$
x(t)\xrightarrow{ 吸 }x(s)= 吸 \mathcal{L}[x(t)]
$$

将(9.1/0)式和(9.5)式比较一下就可发现，单边和双边拉普拉斯变换在定义上的不同在于积分的下限。双边拉普拉斯变换决定于 $ t=-\infty $到 $ t=+\infty $的整个信号，而单边拉普拉斯变换仅仅决定于 $ t=0^{-} $到 $ \infty $的信号。这样以来，在t<0时不同，而在 $ t\geq0 $时相同的两个信号，将有不同的双边拉普拉斯变换，而有相同的单边拉普拉斯变换。同理，任何在t<0都为零的信号其双边和单边拉普拉斯变换相等。

因为 $ x(t) $ 的单边拉普拉斯变换就是将信号 $ x(t) $，在 t<0 时将它的值置于 0 时所求得的双边拉普拉斯变换，因此有关双边拉普拉斯变换中的很多细节、概念和结果都能直接适合于单边的情况。例如，利用 9.2 节对右边信号的性质 4，就可得出，(9.170) 式的 ROC 总是位于某个右半平面。单边拉普拉斯反变换的求取也与双边变换是相同的，只是单边变换的 ROC 一定总是在右半面。

#### 9.9.1 单边拉普拉斯变换举例 {#sec:9-9-1}

为了说明单边拉普拉斯变换，考虑下面这些例子：

**例 9.32 考虑信号 $ x(t) $**

$$
x(t)=\frac{t^{n-1}}{(n-1)!}\mathrm{e}^{-a}u(t)
$$

因为 $ x(t)=0, t<0 $，所以 $ x(t) $ 的单边和双边拉普拉斯变换是一致的。于是，由表9.2可得

$$
\mathcal{D}(s)=\frac{1}{(s+a)^{\pi}},\qquad\mathcal{D}\{s\}>-a
$$

**例 9.33 考虑信号 $ x(t) $**

$$
x(t)=\mathrm{e}^{-a(t+1)}u(t+1)
$$

这个信号的双边变换 $ X(s) $ 可由例 9.1 和时移性质 (9.5.2 节) 求得为

$$
X(s)=\frac{\mathrm{e}^{s}}{s+a},\qquad\mathcal{R}_{s}|_{s}|>-a
$$

与此对照的是，其单边变换是

$$
\mathcal{X}(s)=\int_{0^{-}}^{\infty}\mathrm{e}^{-a(t+1)}u(t+1)\mathrm{e}^{-a}\mathrm{d}t=\int_{0^{-}}^{\infty}\mathrm{e}^{-a}\mathrm{e}^{-t(s+a)}\mathrm{d}t=\mathrm{e}^{-a}\frac{1}{s+a},\qquad\mathcal{R e}\{s\vert>-\alpha
$$

因此，这个例子的单边和双边拉普拉斯变换是明显不同的。事实上，应该将 $ \mathcal{X}(s) $看作不是 $ x(t) $，而是 $ x(t)u(t) $的双边变换，这就与先前关于单边变换就是置一个在 $ t<0^{-} $时为零的信号的双边变换这一结论一致了。

例 9.34 考虑下面信号 $ x(t) $:

$$
x(t)=\delta(t)+2u_{1}(t)+\mathbf{e}^{t}u(t)
$$

因为 $ x(t)=0, t<0 $，并且在积分区间内包括了在原点的奇异函数，所以 $ x(t) $ 的单边变换与双边变换相同。根据表9.2的变换对15， $ u_{n}(t) $ 的双边变换是 $ s^{n} $，所以有

$$
\mathcal{R}(s)\:=\:X(s)\:=\:1+2s+\frac{1}{s-1}=\frac{s(2s-1)}{s-1},\qquad\mathcal{R}|s|>1
$$

例9.35 考虑如下单边拉普拉斯变换：

$$
\mathcal{A}(s)=\frac{1}{(s+1)(s+2)}
$$

在例9.9中已经讨论过一个双边拉普拉斯变换的反变换问题，其代数表示式与(9.179)式完全一样，不过对几种不同的ROC来做的。对于单边变换，ROC一定位于 $ \mathcal{H}(s) $的最右边极点的右边的右半面，也即在这个情况下ROC由全部 $ \mathcal{H}(s) > -1 $的点 $ s $所组成。然后，就完全和例9.9一样，将这个单边变换求反变换而得

$$
x(t)=[\mathrm{e}^{-t}-\mathrm{e}^{-2t}]u(t),\quad t>0^{-}
$$

这里要强调，单边拉普拉斯变换所提供的仅为 $ t>0^{-} $时，信号的有关信息。

例 9.36 考虑如下单边变换：

$$
\mathcal{A}(s)=\frac{s^{2}-3}{s+2}
$$

因为 $ \mathcal{A}(s) $ 分子的阶不是严格地小于分母的阶，所以可将 $ \mathcal{A}(s) $ 展开为

$$
\mathcal{X}(s)=A+B s+\frac{C}{s+2}
$$

令(9.181)式和(9.182)式相等，并通分约去分母可得

$$
s^{2}-3=\big(A+\mathcal{B}s\big)\big(s+2\big)+C
$$

令左右两边同 s 方次的系数相等，就有

$$
\mathcal{X}(s)=-2+s+\frac{1}{s+2}
$$

其 ROC 为 $ \mathcal{R}\{s\} > -2 $。将每一项求反变换可得

$$
x(t)=-2\delta(t)+u_{1}(t)+\mathrm{e}^{-2t}u(t),\qquad t>0^{-}
$$

#### 9.9.2 单边拉普拉斯变换性质 {#sec:9-9-2}

和双边拉普拉斯变换一样，单边拉普拉斯变换也有许多重要的性质，其中有一些与双边

变换是相同的，而另有几个则有明显的不同。表9.3综合了这些性质。要注意的是，对每个信号的单边拉普拉斯变换并没有另辟一列明确地指出它们的ROC，这是由于任何单边拉普拉斯变换的ROC总是某一右半面的缘故。例如，一个有理单边拉普拉斯变换的ROC总是在最右边极点的右边。

Table: 表9.3 单边拉普拉斯变换性质 {#tbl:9-3}

| 性质 | 信号 | 单边拉普拉斯变换 |
| --- | --- | --- |
|  | $ x(t) $\n $ x_1(t) $\n $ x_2(t) $ | $ \mathcal{X}(s) $\n $ \mathcal{X}_1(s) $\n $ \mathcal{X}_2(s) $ |
| 线性 | $ ax_1(t) + bx_2(t) $ | $ a\mathcal{X}_1(s) + b\mathcal{X}_2(s) $ |
| s域平移 | $ e^{s_0t}x(t) $ | $ \mathcal{X}(s - s_0) $ |
| 时域尺度变换 | $ x(at), a > 0 $ | $ \frac{1}{a}\mathcal{X}\left(\frac{s}{a}\right) $ |
| 共轭 | $ x \ast (t) $ | $ \mathcal{X}^*(s^*) $ |
| 卷积[假设 $ t < 0 $, $ x_1(t) $和 $ x_2(t) $均为零] | $ x_1(t) \ast x_2(t) $ | $ \mathcal{X}_1(s)\mathcal{X}_2(s) $ |
| 时域微分 | $ \frac{d}{dt}x(t) $ | $ s\mathcal{X}(s) - x(0^- $) |
| s域微分 | $ -tx(t) $ | $ \frac{d}{ds}\mathcal{X}(s) $ |
| 时域积分 | $ \int_0^t x(\tau)d\tau $ | $ \frac{1}{s}\mathcal{X}(s) $ |

若 $ x(t) $ 在 t=0 不包含任何冲激或高阶奇异函数，则

$$
x(0^{+})=\lim_{s\to\infty}s 实 (s)
$$

$$
\lim_{t\to\infty}x(t)=\lim_{s\to0}s\mathcal{A}(s)
$$

将表9.3和表9.1作一对比可见，单边拉普拉斯变换的收敛域ROC总是在右半面，线性、s域平移、时域尺度变换，共轭和s域微分等性质都与双边变换是一样的。9.5.10节的初值与终值定理对单边拉普拉斯变换也成立 $ ^{①} $。这些性质的推导也与双边变换情况相同。

单边变换的卷积性质也与双边变换情况十分类似。这个性质说的是，若

$$
x_{1}(t)=x_{2}(t)=0,\mathrm{ 对  全  部 }t<0
$$

则

$$
x_{1}(t)\ast x_{2}(t){\overset{\mathcal{H}}{\twoheadrightarrow}}\mathcal{X}_{1}(s)\mathcal{X}_{2}(s)
$$

因为在(9.186)式的条件下， $ x_{1}(t) $ 和 $ x_{2}(t) $ 的单边变换和双边变换是一样的，所以就可以立即由双边变换的卷积性质得出(9.187)式。因此，只要是输入在 t<0 为零时处理因果的 LTI 系统（对此，系统函数既是单位冲激响应的双边，又是单边的拉普拉斯变换），那么在这一章所建立并应用的系统分析方法和系统函数的代数属性勿需任何变化都适用于单边拉普拉斯变换

换。表9.3的积分性质就是一个例子，若 $ x(t)=0 $，t<0，则

$$
\int_{0^{-}}^{t}x(\tau)\mathrm{d}\tau=x(t)*u(t)\xrightarrow{ 负 }\mathcal{X}(s)\mathcal{U}(s)=\frac{1}{s}\mathcal{X}(s)
$$

作为第二种情况，考虑下面这个例子。

例 9.37 假设由下列微分方程描述的一个因果 LTI 系统

$$
\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}+3\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+2y\left(t\right)=x\left(t\right)
$$

具有初始松弛条件。利用(9.133)式，可求得该系统的系统函数是

$$
\mathcal{H}(s)=\frac{1}{s^{2}+3s+2}
$$

设系统的输入是 $ x(t)=\alpha u(t) $。这时，输出 $ y(t) $ 的单边（和双边）拉普拉斯变换是

$$
\begin{aligned}{\mathcal{R}(s)}&{{}=\mathcal{H}(s)\mathcal{R}(s)=\frac{\alpha}{s(s+1)(s+2)}}\\ {}&{{}=\frac{\alpha/2}{s}-\frac{\alpha}{s+1}+\frac{\alpha/2}{s+2}}\\ \end{aligned}
$$

将例9.32用到(9.191)式中的每一项，得到

$$
y(t)=a\left[\frac{1}{2}-\mathrm{e}^{-t}+\frac{1}{2}\mathrm{e}^{-2t}\right]u(t)
$$

重要的是要注意，单边拉普拉斯变换的卷积性质仅在 $ (9.187) $式中 $ x_{1}(t) $和 $ x_{2}(t) $两者在 $ t<0 $都为零时才成立。这就是说，虽然 $ x_{1}(t)*x_{2}(t) $的双边拉普拉斯变换总是等于 $ x_{1}(t) $和 $ x_{2}(t) $的双边拉普拉斯变换的乘积，但是如果 $ x_{1}(t) $或 $ x_{2}(t) $中有一个在 $ t<0 $时不为零，一般来说 $ x_{1}(t)*x_{2}(t) $的单边拉普拉斯变换不等于各自单边拉普拉斯变化的乘积。（见习题9.39）。

单边和双边变换的性质之间一个特别重要的差别是微分性质。考虑某一信号 $ x(t) $，其单边拉普拉斯变换为 $ \mathcal{X}(s) $，那么根据分部积分法可求得 $ dx(t)/dt $的单边变换为

$$
\begin{aligned}\int_{0^{-}}^{\infty}\frac{\mathrm{d}x\left(t\right)}{\mathrm{d}t}\mathrm{e}^{-s t}\mathrm{d}t&=\left.x(t)\mathrm{e}^{-s t}\right|_{0}^{\infty}+s\int_{0}^{\infty}\dot{x}\left(t\right)\mathrm{e}^{-s t}\mathrm{d}t\\&=\left.s\mathcal{X}(s)-x(0^{-})\right.\end{aligned}
$$

同理，再次利用分部积分又可求得 $ \mathrm{d}^{2}x(t)/\mathrm{d}t^{2} $ 的单边拉普拉斯变换，即

$$
s^{2}\mathcal{X}(s)-s x(0^{-})-x^{\prime}(0^{-})
$$

式中 $ x'(0^{-}) $ 为 $ x(t) $ 的导数在 $ t=0^{-} $ 的值。显而易见，可以继续这一过程而得到高阶导数的单边拉普拉斯变换。

#### 9.9.3 利用单边拉普拉斯变换求解微分方程 {#sec:9-9-3}

单边拉普拉斯变换的一个主要应用是在求解具有非零初始条件的线性常系数微分方程上，现用下面例子来说明它。

例 9.38 考虑由(9.189)式的微分方程表征的系统，其初始条件为

$$
y(0^{-})=\beta,\quad y^{\prime}(0^{-})=\gamma
$$

设 $ x(t)=au(t) $。那么在(9.189)式两边应用单边拉普拉斯变换，可得

$$
s^{2}\mathcal{A}\left(s\right)-\beta s-\gamma+3s\mathcal{A}\left(s\right)-3\beta+2\mathcal{A}\left(s\right)=\frac{\alpha}{s}
$$

或者

$$
\textcircled{y}\left(s\right)\;=\;\frac{\beta(s+3)}{(s+1)(s+2)}+\frac{\gamma}{(s+1)(s+2)}+\frac{\alpha}{s(s+1)(s+2)}
$$

式中 $ (s) $ 是 $ y(t) $ 的单边拉普拉斯变换。

参照例9.37，特别是(9.191)式可以看出，(9.197)式右边最后一项就是当(9.195)式的初始条件均为零 $ \beta=\gamma=0 $时系统响应的单边拉普拉斯变换。也就是说，最后一项代表了由(9.189)式描述的因果LTI系统在初始松弛条件下的响应。这个响应常称作零状态响应，也即当初始状态[(9.195)式的一组初始条件]为零时的响应。

对于(9.197)式右边的头两项也可作出类似的解释。这两项所代表的是当输入为零 $ (a=0) $时，该系统响应的单边拉普拉斯变换。这个响应常称作零输入响应。注意，零输入响应是初始条件值的线性函数（即， $ \beta $和 $ \gamma $的值加大一倍，零输入响应也跟着加倍）。再者， $ (9.197) $式对于具有非零初始条件的线性常系数微分方程的解说明了一个重要事实，即总的响应就是零状态响应和零输入响应的叠加。零状态响应是将初始置于零所得到的响应，也即一个由该微分方程定义的LTI系统在初始松弛条件下的响应。零输入响应则是输入为零，系统对初始条件的响应。在习题9.20，9.40和9.66中还能找到其它的例子。

最后，对于任何 $ \alpha, \beta $ 和 $ \gamma $ 值，当然都能将 $ \mathcal{U}(s) $ 展开成部分分式，而求反变换得出 $ y(t) $。例如，若 $ \alpha = 2 $， $ \beta = 3 $ 和 $ \gamma = -5 $，那么 (9.197) 式部分分式展开的结果就是

$$
\mathcal{Y}(s)\;=\;{\frac{1}{s}}-{\frac{1}{s+1}}+{\frac{3}{s+2}}
$$

对每一项应用例9.32的结果就有

$$
y(t)=[1-\mathrm{e}^{-t}+3\mathrm{e}^{-2t}]u(t),\qquad t>0
$$

### 9.10 小结 {#sec:9-10}

这一章讨论并研究了拉普拉斯变换，它可以看成是傅里叶变换的一种推广。在LTI系统的分析和研究中，拉普拉斯变换是一种特别有用的分析工具。由于拉普拉斯变换具有的性质，LTI系统，其中包括由线性常系数微分方程表示的系统，都能够利用代数运算在变换域中进行表征和分析。另外，系统函数的代数属性为分析LTI系统的互联和由微分方程描述的LTI系统方程图表示的构成都提供了一个方便的工具。

对于具有有理拉普拉斯变换的信号与系统，变换往往很方便地用在复平面内标出零点和极点的位置，并指出它们的收敛域来表示。从零极点图上，傅里叶变换，除一个常数因子外，可以用几何的方法求得。因果性，稳定性以及其它的一些特征也很容易地从极点位置和有关收敛域的了解中得以识别。

本章主要关注的是双边拉普拉斯变换，同时也介绍了略有不同的另一种拉普拉斯变换形式，即单边拉普拉斯变换。单边拉普拉斯变换能够看作是在 $ t=0^{-} $以前为零的信号的双边拉普拉斯变换。这种单边拉普拉斯变换在求解具有非零初始条件的线性常系数微分方程中是特别有用的。

**习题**

习题的第一部分属基本题，答案在书末给出。余下的三部分题分属基本题，深入题和扩充题。

**基本题（附答案）**

9.1 对下列每个积分，给出保证积分收敛的实参数 $ \sigma $ 值：

(a) $ \int_{0}^{\infty} e^{-5t} e^{-(\sigma + j\omega)t} dt $ (b) $ \int_{-\infty}^{0} e^{-5t} e^{-(\sigma + j\omega)t} dt $ (c) $ \int_{-5}^{5} e^{-5t} e^{-(\sigma + j\omega)t} dt $ (d) $ \int_{-\infty}^{\infty} e^{-5t} e^{-(\sigma + j\omega)t} dt $ (e) $ \int_{-\infty}^{\infty} e^{-5|t|} e^{-(\sigma + j\omega)t} dt $ (f) $ \int_{-\infty}^{0} e^{-5|t|} e^{-(\sigma + j\omega)t} dt $

### 9.2 考虑信号 {#sec:9-2-2}

$$
x(t)=\mathrm{e}^{-5t}u(t-1)
$$

其拉普拉斯变换记为 $ X(s) $

(a) 利用(9.3)式求 $ X(s) $，并给出它的 $ \mathrm{ROC} $

(b) 确定有限数 A 和 $ t_{0} $，以使 $ g(t) $

$$
g(t)=A\mathrm{e}^{-5t}u(-t-t_{0})
$$

的拉普拉斯变换 $ G(s) $ 与 $ X(s) $ 有相同的代数式。对应于 $ G(s) $ 的 ROC 是什么？

9.3 考虑信号

$$
x(t)=\mathrm{e}^{-5t}u(t)+\mathrm{e}^{-\beta t}u(t)
$$

其拉普拉斯变换记为 $ X(s) $。若 $ X(s) $ 的 ROC 是 $ \mathbb{R}\{s\} > -3 $，应在 $ \beta $ 的的实部和虚部上施加什么限制？9.4 对于 $ x(t) $

$$
x(t)=\left\{\begin{aligned}{}&{{}\mathrm{e}^{t}\mathrm{s i n}2t,\quad}&{}&{{}t\leqslant0}\\ {}&{{}0,\quad}&{}&{{}t>0}\\ \end{aligned}\right.
$$

的拉普拉斯变换指出它的极点位置及其 ROC。

9.5 对下列每个信号拉普拉斯变换的代数表示式，确定位于有限 s 平面的零点个数和在无限远点的零点个数：

(a) $ \frac{1}{s+1}+\frac{1}{s+3} $ (b) $ \frac{s+1}{s^{2}-1} $ (c) $ \frac{s^{3}-1}{s^{2}+s+1} $

9.6 已知一个绝对可积的信号 $ x(t) $ 有一个极点在 s=2，试回答下列问题：

(a) $ x(t) $ 可能是有限持续期的吗？ (b) $ x(t) $ 是左边的吗？

(c) $ x(t) $ 是右边的吗？ (d) $ x(t) $ 是双边的吗？

9.7 有多少个信号，它们的拉普拉斯变换在其收敛域内都有如下表示式的拉普拉斯变换：

$$
\frac{(s-1)}{(s+2)(s+3)(s^{2}+s+1)}
$$

9.8 设 $ x(t) $ 是某一信号，它有一个有理的拉普拉斯变换总共具有两个极点在 s = -1 和 s = -3。若 $ g(t) = e^{2t}x(t) $，其傅里叶变换 $ G(j\omega) $ 收敛，请问 $ x(t) $ 是否是左边的，右边的，或是双边的？

9.9 已知

$$
\mathrm{e}^{-\alpha t}u(t)\overset{\mathcal{L}}{\leftrightarrow}\frac{1}{s+a},\qquad\mathcal{R}_{0}\{s\}>{\mathcal{R}_{0}}\{-a\}
$$

求

$$
X(s)=\frac{2(s+2)}{s^{2}+7s+12},\qquad\mathcal{R}\{s\}>-3
$$

的反变换。

9.10 根据相应的零极点图，利用傅里叶变换模的几何求值方法，确定下列每个拉普拉斯变换其相应的傅里叶变换的模特性是否近似为低通，高通或带通：

(a)

$$
H_{1}(s)=\frac{1}{(s+1)(s+3)},\qquad\mathcal{R}\vert_{s}\vert>-1
$$

(b)

$$
H_{2}(s)=\frac{s}{s^{2}+s+1},\qquad\mathcal{R}_{s}|_{s}|>-\frac{1}{2}
$$

$$
H_{3}(s)=\frac{s^{2}}{s^{2}+2s+1},\quad\mathcal{R}(s)>-1
$$

9.11 利用零极点图的几何求值方法，确定信号的拉普拉斯变换为

$$
X(s)=\frac{s^{2}-s+1}{s^{2}+s+1},\qquad\mathcal{R}_{\infty}|s|>-\frac{1}{2}
$$

的傅里叶变换的模特性。

9.12 关于信号 $ x(t) $，假设已知下面三点：

1. $ x(t)=0 $, t<0

2. $ x(k/80)=0 $, k=1, 2, 3, $ \cdots $

$$
3.x\left(1/160\right)=\mathrm{e}^{-120}
$$

设 $ X(s) $ 为 $ x(t) $ 的拉普拉斯变换，确定下面哪种说法是与给出的有关 $ x(t) $ 信息相一致的：

(a) $ X(s) $ 在有限 s 平面内仅有一个极点。

(b) $ X(s) $ 在有限 s 平面内仅有两个极点。

(c) $ X(s) $在有限s平面内多于两个极点

### 9.13 设 $ g(t) $ 为 {#sec:9-13}

$$
g(t)=x(t)+\alpha x(-t)
$$

式中

$$
x(t)=\beta\mathrm{e}^{-\tau}u(t)
$$

$ g(t) $的拉普拉斯变换是

$$
G(s)=\frac{s}{s^{2}-1},\quad-1<\mathcal{R}\{s\}<1
$$

试确定 $ \alpha $ 和 $ \beta $ 的值？

9.14 关于信号 $ x(t) $ 及其拉普拉斯变换 $ X(s) $ 给出如下条件：

1. $ x(t) $ 是实值的偶信号。

2. 在有限 s 平面内， $ X(s) $ 有 4 个极点而没有零点。

3. $ X(s) $ 有一个极点在 $ s = (1/2)e^{j\pi/4} $

4. $ \int_{-\infty}^{\infty} x(t) dt = 4 $

试确定 $ X(s) $ 和它的 ROC。

9.15 有两个右边信号 $ x(t) $ 和 $ y(t) $，满足下面微分方程：

$$
\frac{\mathrm{d}x(t)}{\mathrm{d}t}=-2y(t)+\delta(t)
$$

和

$$
\frac{\mathrm{d}y(t)}{\mathrm{d}t}=2x(t)
$$

试确定 $ Y(s) $ 和 $ X(s) $ 及其收敛域。

9.16 有一单位冲激响应为 $ h(t) $ 的因果 LTI 系统 S，其输入 $ x(t) $ 和输出 $ y(t) $ 由下面线性常系数微分方程所关联：

$$
\frac{\mathrm{d}^{3}y(t)}{\mathrm{d}t^{3}}+\left(1+\alpha\right)\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}+\alpha\left(\alpha+1\right)\frac{\mathrm{d}y(t)}{\mathrm{d}t}+\alpha^{2}y(t)=x(t)
$$

(a) 若

$$
g(t)=\frac{\mathrm{d}h(t)}{\mathrm{d}t}+h(t)
$$

$ G(s) $ 有多少个极点？

(b) 对于实参数 a 为何值，才能保证系统 S 是稳定的？

9.17 有一因果 LTI 系统 S，其方框图表示如图 P9.17 所示，试确定描述该系统输入 $ x(t) $ 到输出 $ y(t) $ 的微分方程。

9.18 考虑在习题3.20所讨论的 RLC 电路所代表的因果 LTI 系统。

(a) 确定 $ H(s) $ 并给出它的收敛域。答案应与系统是因果和稳定的条件一致。

(b) 利用 $ H(s) $ 的零极点图和傅里叶变换模特性的几何求值法，判断对应的傅里叶变换的模特性是否近似为一个低通，高通或带通特性。

![图像（物理页 546，第 1 幅）](../Figures/fig-p0546-01.jpg){#fig:p546-1}

**图 P9.17**

(c) 若将 R 的值改变为 $ 10^{-3}\Omega $，试确定 $ H(s) $ 并给出它的收敛域。

(d) 利用在(c)中所得 $ H(s) $ 的零极点图和傅里叶变换模特性的几何求值法，判断对应的傅里叶变换的模特性是否近似为一个低通，高通或带通特性。

9.19 确定下列各信号的单边拉普拉斯变换，并给出相应的收敛域：

(a) $ x(t) = \mathrm{e}^{-2t} u(t+1) $ (b) $ x(t) = \delta(t+1) + \delta(t) + \mathrm{e}^{-2(t+3)} u(t+1) $ (c) $ x(t) = \mathrm{e}^{-2t} u(t) + \mathrm{e}^{-4t} u(t) $

9.20 考虑习题 3.19 的 RL 电路。

(a) 当输入电流 $ x(t) = e^{-2t} u(t) $ 时，确定该电路的零状态响应。

(b) 已知 $ y(0^{-}) = 1 $ 确定该电路在 $ t > 0^{-} $ 时的零输入响应。

(c) 当输入电流 $ x(t) = e^{-2t} u(t) $，初始条件同(b)时，确定电路的输出。

**基本题**

9.21 确定下列时间函数的拉普拉斯变换，收敛域及零极点图：

(a) $ x(t) = \mathrm{e}^{-2t} u(t) + \mathrm{e}^{-3t} u(t) $

(b) $ x(t) = \mathrm{e}^{-4t} u(t) + \mathrm{e}^{-5t} (\sin 5t) u(t) $

(c) $ x(t) = \mathrm{e}^{2t} u(-t) + \mathrm{e}^{3t} u(-t) $

(d) $ x(t) = t \mathrm{e}^{-2|t|} $

(e) $ x(t) = |t| e^{-2|t|} $

(f) $ x(t) = |t| e^{2t} u(-t) $

(g) $ x(t) = \left\{ \begin{array}{ll} 1, & 0 \leqslant t \leqslant 1 \\ 0, & \text{其余 } t \end{array} \right. $

(h) $ x(t) = \left\{ \begin{array}{ll} t, & 0 \leqslant t \leqslant 1 \\ 2 - t, & 1 \leqslant t \leqslant 2 \end{array} \right. $

(i) $ x(t) = \delta(t) + u(t) $

(j) $ x(t) = \delta(3t) + u(3t) $

9.22 对下列每个拉普拉斯变换及其收敛域，确定时间函数 x(t)：

(a) $ \frac{1}{s^{2}+9} $, $ \mathcal{R}_{0}|s|>0 $

(b) $ \frac{s}{s^{2}+9} $, $ \mathcal{R}_{0}|s|<0 $

(c) $ \frac{s+1}{(s+1)^{2}+9} $, $ \mathcal{R}_{0}|s|<-1 $

(d) $ \frac{s+2}{s^{2}+7s+12} $, -4< $ \mathcal{R}_{0} $|s\}<-3

(e) $ \frac{s+1}{s^{2}+5s+6} $, -3< $ \mathcal{R}_{0} $|s\}<-2

(f) $ \frac{(s+1)^{2}}{s^{2}-s+1} $, $ \mathcal{R}_{0}|s|>\frac{1}{2} $

(g) $ \frac{s^{2}-s+1}{(s+1)^{2}} $, $ \mathcal{R}_{0}|s|>-1 $

9.23 对于下面关于 $ x(t) $ 的每一种说法，和图 P9.23 中 4 个零极点图中的每一个，确定在 ROC 上相应的限制：

1. $ x(t)e^{-3t} $ 是绝对可积的。

2. $ x(t) \cdot (\mathrm{e}^{-t} u(t)) $ 是绝对可积的。

$$
3.x(i)=0,\;t>1
$$

4. $ x(t)=0, t<-1 $

![图像（物理页 547，第 1 幅）](../Figures/fig-p0547-01.jpg){#fig:p547-1}

**图 P9.23**

9.24 整个这个题目都认为拉普拉斯变换的收敛域总是包括 $ j\omega $ 轴。

(a) 考虑一信号 $ x(t) $，其傅里叶变换为 $ X(j\omega) $，而拉普拉斯变换为 $ X(s)=s+1/2 $。画出 $ X(s) $ 的零极点图。另外，对某一给定的 $ \omega $ 画出一个向量，其长度代表 $ |X(j\omega)| $，而其对实轴的角度代表 $ \angle X(j\omega) $。

(b) 利用考查该零极点图和(a)中的向量图，确定另一个不同的拉普拉斯变换 $ X_{1}(s) $，其对应的时间函数是 $ x_{1}(t) $，使之有

$$
\mid X_{1}(\mathrm{j}\omega):=\mid X(\mathrm{j}\omega)
$$

但

$$
x_{1}(t)\neq x(t)
$$

给出零极点图和代表 $ X_{1}(j\omega) $ 的有关向量。

(c) 对于(b)的答案，再检查一下有关的向量图，确定 $ \angle X(j\omega) $和 $ \angle X_{1}(j\omega) $之间的关系。

(d) 确定某一拉普拉斯变换 $ X_{2}(s) $，以使有

$$
\prec X_{2}(\mathrm{j}\omega)=\prec X(\mathrm{j}\omega)
$$

但是 $ x_{2}(t) $ 不是正比于 $ x(t) $ 的。给出 $ X_{2}(s) $ 的零极点图和代表 $ X_{2}(j\omega) $ 的有关向量。

(e) 对于(d)的答案，确定 $ \left|X_{2}(j\omega)\right| $ 和 $ \left|X(j\omega)\right| $ 之间的关系。

(f) 考虑一信号 $ x(t) $，其拉普拉斯变换为 $ X(s) $，零极点图如图 P9.24 所示。确定 $ X_1(s) $，以使得 $ |X(j\omega)| = |X_1(j\omega)| $，而且 $ X_1(s) $ 的全部极点和零点都位于 s 平面的左半面 [即 $ \varnothing |s| < 0 $]。另外，再确定 $ X_2(s) $，以使得 $ X(j\omega) = X_2(j\omega) $，而且 $ X_2(s) $ 的全部极点和零点都位于 s 平面的左半面。

![图像（物理页 547，第 2 幅）](../Figures/fig-p0547-02.jpg){#fig:p547-2}

**图 P9.24**

9.25 利用9.4节所建立的傅里叶变换的几何确定法，对图P9.25中的每个零极点图画出有关傅里叶变换的模特性。

![图像（物理页 548，第 1 幅）](../Figures/fig-p0548-01.jpg){#fig:p548-1}

**(a)**

![图像（物理页 548，第 2 幅）](../Figures/fig-p0548-02.jpg){#fig:p548-2}

**(b)**

![图像（物理页 548，第 3 幅）](../Figures/fig-p0548-03.jpg){#fig:p548-3}

**(c)**

![图像（物理页 548，第 4 幅）](../Figures/fig-p0548-04.jpg){#fig:p548-4}

**(d)**

![图像（物理页 548，第 5 幅）](../Figures/fig-p0548-05.jpg){#fig:p548-5}

(e)

![图像（物理页 548，第 6 幅）](../Figures/fig-p0548-06.jpg){#fig:p548-6}

(t)

**图 P9.25**

9.26 考虑一信号 $ y(t) $，它与两个信号 $ x_{1}(t) $ 和 $ x_{2}(t) $ 的关系是

式中

$$
y(t)=x_{1}(t-2)*x_{2}(-\;t+3)
$$

$$
x_{1}(t)=\mathrm{e}^{-2t}u(t)\quad 和 \quad x_{2}(t)=\mathrm{e}^{-3t}u(t)
$$

已知

$$
\mathrm{e}^{-a t}u\left(t\right){\overset{\mathcal{X}}{\leftrightarrow}}\frac{1}{s+a},\quad\mathcal{R}_{\mathrm{e}}\left|s\right|>a
$$

利用拉普拉斯变换性质，确定 $ y(t) $ 的拉普拉斯变换 $ Y(s) $。

9.27 关于一个拉普拉斯变换为 $ X(s) $ 的实信号 $ x(t) $ 给出下列 5 个条件：

1. $ X(s) $ 只有两个极点。

2、 $ X(s) $在有限s平面没有零点。

3. $ X(s) $ 有一个极点在 s = -1 + j。

4、 $ e^{2t}x(t) $不是绝对可积的。

5. $ X(0)=8 $

试确定 $ X(s) $ 并给出它的收敛域。

9.28 考虑有一 LTI 系统，其系统函数 $ H(s) $ 的零极点图如图 P9.28 所示。

(a) 指出与该零极点图有关的所有可能的 ROC。

(b) 对于(a)中所标定的每个 ROC，给出有关的系统是否是稳定和/或因果的。

9.29 有一 LTI 系统，输入 $ x(t)=\mathrm{e}^{-t}u(t) $，单位冲激响应 $ h(t)=\mathrm{e}^{-2t}u(t) $。

![图像（物理页 549，第 1 幅）](../Figures/fig-p0549-01.jpg){#fig:p549-1}

(a) 确定 $ x(t) $ 和 $ h(t) $ 的拉普拉斯变换。

(b) 利用卷积性质确定输出 y(t) 的拉普拉斯变换 $ Y(s) $。

**图 P9.28**

(c) 由(b)所求得的 $ y(t) $ 的拉普拉斯变换求 $ y(t) $。

(d) 将 $ x(t) $ 和 $ h(t) $ 直接卷积验证 (c) 的结果。

9.30 一个压力计可以用一个 LTI 系统来仿真，对于一个单位阶跃的输入，其响应为 $ (1 - e^{-t} - te^{-t}) u(t) $。现在某一输入 $ x(t) $ 下，观察到的输出是 $ (2 - 3e^{-t} + e^{-3t}) u(t) $。

对于这个已观察到的结果，确定该压力计的真正压力输入(作为时间的函数)。

9.31 有一连续时间 LTI 系统，其输入 $ x(t) $ 和输出 $ y(t) $ 由下列微分方程所关联：

$$
\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}-\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}-2y\left(t\right)=x\left(t\right)
$$

设 $ X(s) $ 和 $ Y(s) $ 分别是 $ x(t) $ 和 $ y(t) $ 的拉普拉斯变换， $ H(s) $ 是系统单位冲激响应 $ h(t) $ 的拉普拉斯变换。

(a) 求 $ H(s) $ 作为 s 的两个多项式之比，画出 $ H(s) $ 的零极点图。

(b) 对下列每一种情况求 $ h(t) $:

(i) 系统是稳定的。 (ii) 系统是因果的。 (iii) 系统既不稳定又不是因果的。

9.32 一个单位冲激响应为 $ h(t) $ 的因果 LTI 系统有下列性质：

(a) 当系统的输入为 $ x(t) = e^{2t} $，对全部 t 时，输出对全部 t 是 $ y(t) = (1/6)e^{2t} $

(b) 单位冲激响应 $ h(t) $ 满足下列微分方程：

$$
\frac{\mathrm{d}h\left(t\right)}{dt}+2h\left(t\right)=\left(\mathrm{e}^{-4t}\right)u\left(t\right)+bu\left(t\right)
$$

这里 b 是一个未知常数。

确定该系统的系统函数 $ H(s) $，以与上述性质相符。在答案中不应该有未知常数，也就是说该未知常数 b 不应该出现在答案中。

9.33 有一因果 LTI 系统的系统函数是

$$
H(s)\;=\;{\frac{s+1}{s^{2}+2s+2}}
$$

当输入 $ x(t) $为

$$
x(t)=\mathrm{e}^{-|t|},\qquad-\infty<t<\infty
$$

求出并画出响应 $ y(t) $

9.34 假设关于一个单位冲激响应为 $ h(t) $ 和有理系统函数为 $ H(s) $ 的因果而稳定的 LTI 系统给出下列信息：

$$
1.H(1)=0.2
$$

2. 当输入为 $ u(t) $ 时，输出是绝对可积的。

3. 当输入为 $ t u(t) $ 时，输出不是绝对可积的。

4. 信号 $ \mathrm{d}^{2}h(t)/\mathrm{d}t^{2}+2\mathrm{d}h(t)/\mathrm{d}t+2h(t) $ 是有限长的。

5. $ H(s) $ 在无限远点只有一个零点。

确定 $ H(s) $及其收敛域。

9.35 一个因果 LTI 系统的输入 $ x(t) $ 和输出 $ y(t) $ 是通过由图 P9.35 的方框图来表示的。

(a) 求联系 $ y(t) $ 和 $ x(t) $ 的微分方程。

(b) 该系统是稳定的吗？

9.36 本题要讨论输入为 $ x(t) $，输出为 $ y(t) $ 和系统函数为

$$
H(s)=\frac{2s^{2}+4s-6}{s^{2}+3s+2}
$$

![图像（物理页 550，第 1 幅）](../Figures/fig-p0550-01.jpg){#fig:p550-1}

**图 P9.35**

的因果 LTI 系统 S 的各种方框图表示的结构。为了导出 S 的直接型方框图表示，首先考虑一因果 LTI 系统 $ S_{1} $，其输入与系统 S 的输入相同为 $ x(t) $，但它的系统函数为 $ H_{1}(s) $

$$
H_{1}(s)=\frac{1}{s^{2}+3s+2}
$$

若系统 $ S_{1} $ 的输出记为 $ y_{1}(t) $，则 $ S_{1} $ 的直接型方框图表示就如图 P9.36 所示。图中信号 $ e(t) $ 和 $ f(t) $ 分别代表两个积分器的输入。

(a) 将 $ y(t) $ (系统 S 的输出) 表示成 $ y_{1}(t) $, $ \mathrm{d}y_{1}(t)/\mathrm{d}t $ 和 $ \mathrm{d}^{2}y_{1}(t)/\mathrm{d}t^{2} $ 的线性组合。

(b) $ \mathrm{dy}_{1}(t)/\mathrm{d}t $ 是如何与 $ f(t) $ 相关联的？

(c) $ \mathrm{d}^{2}y_{1}(t)/\mathrm{d}t^{2} $ 是如何与 e(t) 相关联的？

(d) 将 $ y(t) $ 表示成 $ \mathrm{e}(t) $， $ f(t) $ 和 $ y_{1}(t) $ 的线性组合。

![图像（物理页 550，第 2 幅）](../Figures/fig-p0550-02.jpg){#fig:p550-2}

(e) 利用前面部分的结果将 $ S_{1} $ 的直接型方框图表示推广，形成 S 的方框图表示。

(f) 注意到

$$
H(s)=\left(\frac{2(s-1)}{s+2}\right)\left(\frac{s+3}{s+1}\right)
$$

画出将 S 作为两个子系统级联的方框图表示。

(g) 注意到

$$
H(s)=2+\frac{6}{s+2}-\frac{8}{s+1}
$$

画出将 S 作为三个子系统并联的方框图表示。

9.37 画出具有下列系统函数的因果 LTI 系统的直接型表示：

$$
\mathrm{(a)}~H_{1}(s)=\frac{s+1}{s^{2}+5s+6}\qquad\mathrm{(b)}~H_{2}(s)=\frac{s^{2}-5s+6}{s^{2}+7s+10}\qquad\mathrm{(c)}~H_{3}(s)=\frac{s}{(s+2)^{2}}.
$$

9.38 有一四阶因果 LTI 系统 S，其系统函数为

$$
H(s)=\frac{1}{(s^{2}-s+1)(s^{2}+2s+1)}
$$

（a）证明：对于由四个一阶节级联组成的 S 的直接型表示中一定包含有不是纯实数的系数相乘。

(b) 画出将 S 作为两个二阶系统级联的方框图表示，每一个二阶系统都用直接型表示。在所得到的方框图中不应该有非实数系数的相乘。

(c) 画出将 S 作为两个二阶系统并联的方框图表示，每一个二阶系统都用直接型表示。在所得到的方框图中不应该有非实数系数的相乘。

9.39 设 $ x_{1}(t) $ 和 $ x_{2}(t) $ 为

$$
x_{1}(t)=\mathrm{e}^{-2t}u(t)\quad 和 \quad x_{2}(t)=\mathrm{e}^{-3(t+1)}u(t+1)
$$

(a) 对 $ x_{1}(t) $ 求单边拉普拉斯变换 $ \mathcal{L}_{1}(s) $ 和双边拉普拉斯变换 $ X_{1}(s) $

(b) 对 $ x_{2}(t) $ 求单边拉普拉斯变换 $ \mathcal{X}_{2}(s) $ 和双边拉普拉斯变换 $ X_{2}(s) $

(c) 取 $ X_{1}(s)X_{2}(s) $ 的双边反变换求信号 $ g(t)=x_{1}(t)*x_{2}(t) $

(d) 证明 $ \mathcal{X}_{1}(s)\mathcal{X}_{2}(s) $ 的单边反变换在 $ t>0^{-} $时不同于 $ g(t) $。

9.40 考虑由下列微分方程表征的系统 S:

$$
\frac{\mathrm{d}^{3}y\left(t\right)}{\mathrm{d}t^{3}}+6\frac{\mathrm{d}^{2}y\left(t\right)}{\mathrm{d}t^{2}}+11\frac{\mathrm{d}y\left(t\right)}{\mathrm{d}t}+6y\left(t\right)=x\left(t\right)
$$

(a) 当输入 $ x(t) = e^{-4t} u(t) $ 时，求该系统的零状态响应。

(b) 已知

$$
y(0^{-})=1,\qquad\frac{\mathrm{d}y(t)}{\mathrm{d}t}\mid_{t=0^{-}}=-1,\qquad\frac{\mathrm{d}^{2}y(t)}{\mathrm{d}t^{2}}\mid_{t=0^{-}}=1
$$

求 $ t>0^{-} $系统的零输入响应。

(c) 当输入为 $ x(t)=\mathrm{e}^{-4t}u(t) $ 和初始条件同(b)所给出时，求系统 S 的输出。

**深入题**

9.41 (a) 证明：若 $ x(t) $ 是偶函数 $ x(t)=x(-t) $，则 $ X(s)=X(-s) $

(b) 证明：若 $ x(t) $ 是奇函数 $ x(t) = -x(-t) $，则 $ X(s) = -X(-s) $

(c) 对于图 P9.41 所示的零极点图，判断有无与一个偶时间函数相对应的零极点图？若有，对这些图指出要求的 ROC。

9.42 判断下列每种说法是真还是假。若是真，为它构造一个有力的证据；若为假，给出一个反例。

(a) $ t^{2}u(t) $ 的拉普拉斯变换在 s 平面的任何地方都不收敛。

(b) $ e^{t^{2}} u(t) $ 的拉普拉斯变换在 s 平面的任何地方都不收敛。

![图像（物理页 552，第 1 幅）](../Figures/fig-p0552-01.jpg){#fig:p552-1}

**(a)**

![图像（物理页 552，第 2 幅）](../Figures/fig-p0552-02.jpg){#fig:p552-2}

**(b)**

![图像（物理页 552，第 3 幅）](../Figures/fig-p0552-03.jpg){#fig:p552-3}

**(c)**

![图像（物理页 552，第 4 幅）](../Figures/fig-p0552-04.jpg){#fig:p552-4}

**(d)**

**图 P9.41**

(c) $ e^{j\omega_{0}t} $ 的拉普拉斯变换在 s 平面的任何地方都不收敛。

(d) $ e^{jw_{0}t} u(t) $ 的拉普拉斯变换在 s 平面的任何地方都不收敛。

(e) |t|的拉普拉斯变换在s平面的任何地方都不收敛。

9.43 设 $ h(t) $ 是一个具有有理系统函数的因果而稳定的 LTI 系统的单位冲激响应

(a) 单位冲激响应为 $ \mathrm{dh}(t)/\mathrm{dt} $ 的系统能保证是因果和稳定的吗？

(b) 单位冲激响应为 $ \int_{-\infty}^{t} h(\tau) \, d\tau $ 的系统能保证是因果和不稳定的吗？

9.44 设 $ x(t) $ 是如下的已采样信号：

$$
x(t)=\sum_{n=0}^{\infty}\mathrm{e}^{-nT}\delta(t-nT)
$$

式中 $ T>0 $。

(a) 求 $ X(s) $，包括它的收敛域。

(b) 画出 $ X(s) $ 的零极点图。

(c) 利用零极点图的几何解释，证明： $ X(j\omega) $ 是周期的。

9.45 对于图 P9.45(a) 的 LTI 系统，已知下列情况：

$$
X(s)=\frac{s+2}{s-2}
$$

$$
x(t)=0,\qquad t>0
$$

和

$$
y(t)=-\frac{2}{3}\mathrm{e}^{2t}u(-t)+\frac{1}{3}\mathrm{e}^{-t}u(t)\quad[ 见图 \mathrm{P9}.45(\mathrm{b})]
$$

![图像（物理页 553，第 1 幅）](../Figures/fig-p0553-01.jpg){#fig:p553-1}

![图像（物理页 553，第 2 幅）](../Figures/fig-p0553-02.jpg){#fig:p553-2}

**图 P9.45**

(a) 求 $ H(s) $ 和它的收敛域。 (b) 求 $ h(t) $。

(c) 若输入为

$$
x(t)=\mathrm{e}^{3t},\qquad-\infty<t<+\infty
$$

利用(a)中求得的系统函数 $ H(s) $，求输出 $ y(t) $。

9.46 设 $ H(s) $ 代表一因果稳定系统的系统函数，该系统的输入是由三项之和组成的，其中之一是一个冲激 $ \delta(t) $，而其余的则是 $ e^{t}u^{t} $ 的复指数形式，这里 $ s_{0} $ 是一个复常数。系统的输出是

$$
y(t)=-6\mathrm{e}^{-t}u(t)+\frac{4}{34}\mathrm{e}^{4t}\cos3t+\frac{18}{34}\mathrm{e}^{4t}\sin3t+\delta(t)
$$

求与这些条件相符的 $ H(s) $

### 9.47 设信号 {#sec:9-47}

$$
y(t)=\mathrm{e}^{-2t}u(t)
$$

是系统函数为

$$
H(s)=\frac{s-1}{s+1}
$$

的因果全通系统的输出。

(a) 求出并画出至少有两种可能的输入 $ x(t) $ 都能产生 $ y(t) $ 。

(b) 若已知

$$
\int_{-\infty}^{\infty}\mid x(t)\mid\mathrm{d}t<\infty
$$

问输入 $ x(t) $是什么？

(c) 如果已知存在某个稳定(但不一定因果)的系统，它若以 $ y(t) $ 作输入，则输出为 $ x(t) $，问这个输入 $ x(t) $ 是什么？求这个滤波器的单位冲激响应，并用直接卷积证明它有所声称的性质[即 $ y(t) * h(t) = x(t) $]。

9.48 一个 LTI 系统 $ H(s) $ 的逆系统是定义成这样一个系统，当它与 $ H(s) $ 级联后所得到的总系统函数为 1，或者说，总的系统单位冲激响应是一个单位冲激函数。

(a) 若用 $ H_{1}(s) $ 记为 $ H(s) $ 逆系统的系统函数，确定 $ H(s) $ 和 $ H_{1}(s) $ 之间一般的代数关系。

(b) 图 P9.48 示出一个稳定，因果系统 $ H(s) $ 的零极点图，试确定它的逆系统的零极点图。

![图像（物理页 553，第 3 幅）](../Figures/fig-p0553-03.jpg){#fig:p553-3}

**图 P9.48**

9.49 · 种称之为最小延时或最小相位系统有时是通过这一说法来定义的：这些系统是因果的且是稳定的，而它们的逆系统也是因果和稳定的。

基于上面的定义，试建立一个论据来说明：一个最小相位系统的系统函数，其全部极点和零点都必须位于 s 平面的左半面 [即, $ \mathcal{R}_{k}\{s\} < 0 $]。

9.50 判断关于 LT1 系统下列每一种说法是否是对的。若一种说法是对的，给出一个有力的证据；若不对，给出一个反例。

(a) 一个稳定的连续时间系统其全部极点必须位于 s 平面的左平面 [即, $ S_{1} < 0 $]。

(b) 若一个系统函数的极点数多于零点数，而这个系统是因果的，那么阶跃响应在 t=0 一定连续。

(c) 若一个系统函数的极点数多于零点数，而这个系统不限定是因果的，那么阶跃响应在 t=0 可能不连续。

(d) 一个稳定和因果的系统，其系统函数的全部极点和零点都必须在 s 平面的左半面。

9.51 有一稳定和因果的系统，其单位冲激响应 $ h(t) $ 是实值函数，系统函数为 $ H(s) $。已知 $ H(s) $ 是有理的，它的极点之一在 $ (-1+j) $，零点之一在 $ (3+j) $，并且在无限远点只有两个零点。对于下面每种说法，判断是对，还是错，或者条件不充分而难以置评。

(a) $ h(t) e^{-3t} $ 是绝对可积的。

(b) $ H(s) $ 的 ROC 是 $ \mathcal{R}_{n}|_{S}| > -1 $

(c) 关联系统 S 的输入 $ x(t) $ 和输出 $ y(t) $ 的微分方程可以仅用实系数的形式写出。

(d) $ \lim_{s \to \infty} H(s) = 1 $

(e) $ H(s) $ 不少于4个极点。

(1) 至少存在一个有限的 $ \omega $，有 $ H(j\omega)=0 $。

(g)若系统 S 的输入是 $ e^{3t} \sin t $，输出就是 $ e^{3t} \cos t $。

9.52 正如在9.5节所指出的，拉普拉斯变换的许多性质和推导都和对应的傅里叶变换的性质和推导相类似的。本题将要求导出几个拉普拉斯变换的性质。

细心注意一下在第4章对傅里叶变换有关性质的推导过程，导出下列每个拉普拉斯变换的性质，导出时必须包括有关收敛域的考虑。

(a) 时移(9.5.2节)。

(b) s 域平移(9.5.3 节)。

(c) 时域尺度变换(9.5.4节)。 (d) 卷积性质(9.5.6节)。

9.53 正如在9.5.10节所提到的，初值定理说的是，对一个拉普拉斯变换为 $ X(s) $的信号 $ x(t) $，若 $ x(t)=0,t<0 $，那么 $ x(t) $的初值[即， $ x(0^{t}) $]可以由 $ X(s) $通过关系

$$
x(0^{+})=\operatorname*{l i m}_{s\to\infty}s X(s)
$$

求得。首先注意到，因为 $ x(t)=0, t<0, x(t)=x(t)u(t) $。接下来将 $ x(t) $ 在 $ t=0^{+} $ 展开成泰勒级数，得到

$$
x(t)=\left[x(0+)+x^{(1)}(0+)t+\cdots+x^{(n)}(0+\right)\frac{t^{n}}{n!}+\cdots\bigg]u(t)
$$

式中 $ x^{(n)}(0^{+}) $ 代表 $ x(t) $ 的 n 阶导数在 $ t=0^{+} $ 的值。

(a) 求 $ (P9.53-1) $ 式右边任意项 $ x^{(n)}(0^{+})(t^{n}/n!)u(t) $ 的拉普拉斯变换。(参考例 9.14 有助于求解)。

(b) 由(a)的结果和(P9.53-1)式的展开式，证明 $ X(s) $ 可以表示成

$$
X(s)=\sum_{n=0}^{\infty}x^{(n)}(0^{+})\frac{1}{s^{n+1}}
$$

（c）证明由(b)的结果就可得出(9.110)式。

(d) 利用首先求出 $ x(t) $，对下列各个例子验证初值定理：

(1) $ X(s)=\frac{1}{s+2} $

(2) $ X(s)=\frac{s+1}{(s+2)(s+3)} $

(e) 初值定理的一般形式是说：若 $ x^{(n)}(0^{+})=0 $, n<N, 那么 $ x^{(N)}(0^{+})=\lim_{s\to\infty}s^{N+1}X(s) $。证明这个一般的形式也可由(b)的结果得到。

9.54 有一拉普拉斯变换为 $ X(s) $ 的实值信号 $ x(t) $。

(a) 在(9.56)式两边应用复数共轭，证明 $ X(s)=X^{*}(s^{*}) $。

(b) 根据(a)的结果，证明：若 $ X(s) $ 在 $ s = s_{0} $ 有一个极点（零点），那么在 $ s = s_{0}^{*} $ 也必须有一个极点（零点）；也就是说，对于实值的 $ x(t) $， $ X(s) $ 的极点和零点必须共轭成对地出现，除非它们是在实轴上。

9.55 在9.6节表9.2中列出几个拉普拉斯变换对，并具体地指出从变换对1到9是如何从例9.1和例9.14，以及结合表9.1的各种性质来得到的。

利用表9.1的各个性质，证明变换对从10～16是如何根据表9.2的变换对从1～9来得到的。

9.56 对于某一具体的复数 s，若变换的模是有限的，即若 $ |X(s)| < \infty $，就说这个拉普拉斯变换存在。

证明：变换 $ X(s) $ 在 $ s = s_0 = \sigma_0 + j\omega_0 $ 存在的一个充分条件是

$$
\int_{-\infty}^{+\infty}\mid x(t)\mid\mathrm{e}^{-\sigma_{0}t}\mathrm{d}t<\infty
$$

换句话说，证明 $ x(t) $ 被 $ e^{-\sigma_0 t} $ 指数加权后是绝对可积的。求证时，需要利用复函数 $ f(t) $ 的下面结论：

$ |\int_{a}^{b}f(t)dt|\leqslant\int_{a}^{b}|f(t)|dt $ (P9.56-1)

如果不对(P9.56-1)式作严格证明，你能证明这是可能的吗？

9.51 一个信号 $ x(t) $ 的拉普拉斯变换 $ X(s) $ 有 4 个极点，而零点个数未知；又知信号 $ x(t) $ 在 t=0 有一个冲激。试确定在什么样的有关信息下（如果有），可以提供有关零点的个数及其它们的位置的情况。

9.58 设 $ h(t) $ 是一个具有有理系统函数 $ H(s) $ 的因果而稳定的 LTI 系统的单位冲激响应，证明： $ g(t)= $

$ \mathcal{R}_{0}\{h(t)\} $ 也是一个因果稳定系统的单位冲激响应。

9.59 若 $ \mathcal{P}(s) $ 是 $ x(t) $ 的单边拉普拉斯变换，利用 $ \mathcal{P}(s) $ 求下列各信号的单边拉普拉斯变换：

(a) $ x(t-1) $

(b) $ x(t+1) $

(c) $ \int_{-\infty}^{\infty} x(\tau) d\tau $

(d) $ \frac{d^{3}x(t)}{dt^{3}} $

**扩充题**

9.60 在长途电话通信中，由于被传输的信号在接收端被反射，有时候会遇到回波，回波又经线路被送回来，再次在发射端被反射，又返回到接收端。这样的过程可以用图 P9.60 所示的单位冲激响应系统来仿真，图中已假定只接收到一个回波。参数 T 相当于沿通信信道的单向传播时间。参数 $ \alpha $ 代表在发射端与接收端之间在幅度上的衰减。

![图像（物理页 555，第 1 幅）](../Figures/fig-p0555-01.jpg){#fig:p555-1}

(a) 求该系统的系统函数 $ H(s) $ 及其 $ ROC_{0} $

**图 P9.60**

(b) 从(a)的结果应该看到， $ H(s) $已不是由两个多项式之比组成的。不过，用极点和零点来表示仍是有用的。这里和一般情况相同，零点就是使 $ H(s)=0 $的那些s值，而极点是使 $ \left[1/H(s)\right]=0 $的那些s值。试对(a)中所确定的系统，确定它的零点，并说明它没有任何极点。

(c) 根据(b)的结果，画出 $ H(s) $ 的零极点图。

(d) 通过考查在 s 平面内合适的向量，大致画出该系统频率响应的模特性。

9.61 一个信号 $ x(t) $ 的自相关函数定义为

$$
\phi_{x x}(\tau)=\int_{-\infty}^{\infty}x(t)x(t+\tau)\mathrm{d}t
$$

(a) 求当输入为 $ x(t) $，输出为 $ \phi_{xx}(t) $ 的 LTI 系统 [如图 P9.61(a) 所示] 的单位冲激响应 $ h(t) $ (利用 $ x(t) $ 来表示)。

(b) 根据(a)的结果，求：利用 $ X(s) $ 来表示的 $ \phi_{xx}(\tau) $ 的拉普拉斯变换 $ \Phi_{xx}(s) $；另外将 $ \phi_{xx}(\tau) $ 的傅里叶变换 $ \Phi_{xx}(j\omega) $ 用 $ X(j\omega) $ 来表示。

(c) 如果 x(t) 的拉普拉斯变换 X(s) 有如图 P9.61(b) 所示的零极点图和 ROC，画出 $ \Phi_{xx}(s) $ 的零极点图并指出 ROC。

![图像（物理页 556，第 1 幅）](../Figures/fig-p0556-01.jpg){#fig:p556-1}

**图 P9.61**

9.62 在信号设计和分析的一些应用中，会遇到这样一类信号

$$
\phi_{n}(t)=\mathrm{e}^{-t/2}L_{n}(t)u(t),\;n=0,~1,~2,~\cdots
$$

式中

$$
L_{n}(t)=\frac{\mathrm{e}^{t}}{n!}\frac{\mathrm{d}^{n}}{\mathrm{d}t^{n}}(t^{n}\mathrm{e}^{-t})
$$

(a) 函数 $ L_{n}(t) $ 称为 Laguerre 多项式。为了证明它们事实上具有多项式的形式，试用显式确定出 $ L_{0}(t) $， $ L_{1}(t) $ 和 $ L_{2}(t) $。

(b) 利用表 9.1 的拉普拉斯变换性质和表 9.2 的拉普拉斯变换时，求 $ \phi_{n}(t) $ 的拉普拉斯变换 $ \Phi_{n}(s) $

(c) 用一个单位冲激函数去激励图 P9.62 中的网络可以产生信号集 $ \phi_{n}(t) $。求 $ H_{1}(s) $ 和 $ H_{2}(s) $，使得沿此级联链路的单位冲激响应正是所指出的信号 $ \phi_{n}(t) $。

![图像（物理页 556，第 2 幅）](../Figures/fig-p0556-02.jpg){#fig:p556-2}

**图 P9.62**

9.63 在滤波器设计中，将一个低通滤波器转换到一个高通滤波器，或者相反，往往是可能的，而且也是方便的。现用 $ H(s) $ 代表原滤波器的转移函数，用 $ G(s) $ 代表已被转换的滤波器的转移函数，这样一种通常所用的转换是用 1/s 来代替 s 来构成，即

$$
G(s)=H\Bigl(\frac{1}{s}\Bigr)
$$

(a) 若 $ H(s)=1/(s+\frac{1}{2}) $，画出 $ \left|H(j\omega)\right| $ 和 $ \left|G(j\omega)\right| $。

(b) 确定与 $ H(s) $ 和 $ G(s) $ 有关的线性常系数微分方程。

(c) 现在考虑一般的情况，其中 $ H(s) $ 是与下面一般形式的线性常系数微分方程相联系的转移函数：

$$
\sum_{k=0}^{N}a_{k}\;\frac{\mathrm{d}^{k}y(t)}{\mathrm{d}t^{k}}\;=\;\sum_{k=0}^{N}b_{k}\;\frac{\mathrm{d}^{k}x(t)}{\mathrm{d}t^{k}}
$$

不失一般性，假定上式两边的最高阶导数 N 相等，尽管在任何具体情况下，其中的某些系数可能是零。求 $ H(s) $ 和 $ G(s) $。

(d) 根据(c)的结果，利用(P9.63-1)中的系数，确定与 $ G(s) $ 有关的线性常系数微分方程。

9.64 考虑图 9.27 所示的 RLC 电路，设输入为 $ x(t) $，输出为 $ y(t) $。

(a) 证明：若 R，L 和 C 全部是正的，则这个 LTI 系统是稳定的。

(b) R，L 和 C 互相之间应该有怎样的关系，才能使该系统代表二阶巴特沃兹

9.65 (a) 求图 P9.65 所示 RLC 电路关于 $ v_{i}(t) $ 和 $ v_{0}(t) $ 之间的微分方程。

(b) 假定 $ v_{i}(t) = e^{-3t} u(t) $，利用单边拉普拉斯变换求 t > 0 时的 $ v_{0}(t) $。

9.66 考虑图 P9.66 所示 RL 电路。假设电流 i(t) 在开关位于 A 时已到达稳态。在 t=0，开关由 A 移至 B。

![图像（物理页 557，第 1 幅）](../Figures/fig-p0557-01.jpg){#fig:p557-1}

(a) 求 $ t > 0^{-} $时， $ i(t) $ 和 $ v_{2} $ 之间的微分方程。利用 $ v_{1} $ 为这个微分方程标出初始条件（即， $ i(0^{-}) $ 的值）。

**图 P9.65**

(b) 利用表9.3单边拉普拉斯变换的性质，求出并画出对于下列

的 $ v_{1} $ 和 $ v_{2} $ 时的 $ i(t) $:

(i) $ v_1 = 0\,\text{V} $, $ v_2 = 2\,\text{V} $

(ii) $ v_1 = 4V $, $ v_2 = 0V $

(iii) $ v_1 = 4V $, $ v_2 = 2V $

利用(i)，(ii)和(iii)中的答案，证明： $ i(t) $可以表示成电流的零状态响应和零输入响应之和。

![图像（物理页 557，第 2 幅）](../Figures/fig-p0557-02.jpg){#fig:p557-2}

**图 P9.66**
