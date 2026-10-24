# 两个代数多边形的平铺与 ZFC 一致性

> 研究说明，整理于 2026-10-25。本文引用已有的计算与平铺归约，补充十二位置凹凸编码及正五边形填充的几何论证。本文尚未由证明助手形式验证，也没有核验原始示意图标注的具体 K215 棒长和边数。

可以有效构造两个有限的简单多边形  $P,Q$ ，其中  $Q$  是正五边形，使得在允许平移和旋转、禁止反射的模型中：

$$
\mathrm{Tile}(P,Q)\quad\Longleftrightarrow\quad\mathrm{Con}(\mathrm{ZFC}).
$$

平铺指用全等副本覆盖整个欧氏平面，瓦片内部两两不交。本文证明按下述过程有效定义的一对多边形的存在性，尚未输出全部顶点清单。

## 1. 一致性与不停机

固定通常的 ZFC 形式证明系统；其公理模式实例及有限证明是否合法，均可由有限算法检查。令机器  $M$  枚举全部有限字符串，找到 ZFC 的合法矛盾证明时停机。因此

$$
M\uparrow\ \Longleftrightarrow\ \text{ZFC 没有有限矛盾证明}
\ \Longleftrightarrow\ \mathrm{Con}(\mathrm{ZFC}).
$$

 $M\uparrow$  表示在约定的空白输入上永不停机。这个等价关系不要求预先假设 ZFC 一致。

若使用特定机器 K215，须额外引用精确转移表及校准。固定提交 a61476422532a5d3b7dec11fc7a92751fe0d60f8 的 [发布说明](https://github.com/VladimirReshetnikov/ProveIt/blob/a61476422532a5d3b7dec11fc7a92751fe0d60f8/Computability/BusyBeaver/Research/ZFC/candidate-k215/README.md)、[转移表](https://github.com/VladimirReshetnikov/ProveIt/blob/a61476422532a5d3b7dec11fc7a92751fe0d60f8/Computability/BusyBeaver/Research/ZFC/candidate-k215/k215.tm)及[校准证明](https://github.com/VladimirReshetnikov/ProveIt/blob/a61476422532a5d3b7dec11fc7a92751fe0d60f8/Computability/BusyBeaver/Research/ZFC/candidate-k215/proof.md)给出相应的普通数学论证。本文未重放全部验证材料；一般存在性证明可直接使用上述搜索机。

## 2. 引用的全平面归约

使用标准的“非停机到无预放种子的整个平面 Wang 平铺”的有效归约，得到有限瓦片集  $W(M)$ ，满足

$$
\mathrm{Tile}(W(M))\quad\Longleftrightarrow\quad M\uparrow.
$$

这里需要该方向的等价归约。单纯的算法不可判定性，或从指定初始行出发的计算历史，都不足以替代这一步。经典层级构造排除绕开初始化的伪计算，紧致性将任意大合法图案接成全平面平铺。背景与非停机归约方向见文献 [2] 引言。

再引用 Stade [1] 第 2 节的有效构造，得到一个由  $n\geq5$  个单位正六边形直线连接的长条  $T$  和无向边禁配关系  $R$ ：

$$
\mathrm{Tile}_R(T)\quad\Longleftrightarrow\quad\mathrm{Tile}(W(M)).
$$

本文引用其 Wang→AB→六角长条归约，不重新证明全部状态与桶构造。

该构造的每个禁配对至少有一端属于六种特殊端边

$$
S=\lbrace s_1,\ldots,s_6\rbrace =\lbrace x_1,x_2,y_1,y_2,z_1,z_2\rbrace .
$$

此性质可由 [1] 第 2.1 节的十一类规则及第 2.3 节箭头、三角标记新增的禁配逐项检查。 $R$  按无向标签对理解，故为对称关系。

## 3. 十二位置与正五边形轮廓

取外接圆半径  $\delta=10^{-6}$  的正五边形  $F$ ，对称轴水平，一端穿过顶点，另一端穿过对边中点；将轴上截弦的中点放在原点。设

$$
H=F\cap\lbrace y\geq0\rbrace ,\quad
M_x(x,y)=(-x,y),\quad M_y(x,y)=(x,-y),\quad H'=M_xH.
$$

所以  $F=H\cup M_yH$ 。 $H$  沿截弦左右不对称， $H'$  为其左右镜像。

每条原始边按逆时针边界方向建立局部坐标：从  $(0,0)$  指向  $(1,0)$ ，内侧在上方。安排十二个位置，截弦中点为  $(j/13,0)$ ， $j=1,\ldots,12$ 。前六位置以  $H$  为轮廓，后六位置以  $H'$  为轮廓。

状态  $0$  表示从内侧挖去相应半片；状态  $1$  表示向外增加该半片关于底边的镜像。微小尺度保证特征互相隔离、远离原顶点，六角格中心也保持不变。

对原边标签  $e$ ，定义

$$
b_i(e)=\mathbf1_{\lbrace e=s_i\rbrace },\qquad
b_{13-i}(e)=\mathbf1_{\lbrace (e,s_i)\in R\rbrace },\qquad i=1,\ldots,6.
$$

按这些状态修改长条，所得主多边形记为  $P$ ；取  $Q=F$  为唯一填充块。

## 4. 接触编码的正确性

原边对接时，位置  $i$  对应位置  $13-i$ 。某处双凸，当且仅当

$$
e=s_i\text{ 且 }(f,s_i)\in R,
\quad\text{或}\quad f=s_i\text{ 且 }(e,s_i)\in R.
$$

由对称性与六特殊边的覆盖性质，

$$
\text{某处双凸}\quad\Longleftrightarrow\quad(e,f)\in R.
$$

双凸时，凸起进入对面未挖去的主体，造成内部重叠。合法接触时，凸凹互填，双凹留下完整正五边形洞。

方向检查不能省略。令  $R_\pi(x,y)=(-x,-y)$ ，则

$$
R_\pi H'=M_yH,\qquad R_\pi(M_yH')=H.
$$

因此前六位置的双凹组成  $F$ ，后六位置的双凹组成  $M_xF=R_\pi F$ 。旋转后的同一种填充块即可填洞，不需要反射瓦片。

## 5. 角度锁定与全局网格恢复

首先  $Q$  单独不能平铺：在其顶点，其他正五边形只能贡献顶角或平角，而

$$
108k+180\ell=360,\qquad k\geq1,\quad\ell\geq0
$$

无整数解。故任意  $P,Q$  平铺至少含一块  $P$ 。

 $P$  保留的原角为  $120^\circ$  或  $240^\circ$ 。半五边形的角为  $90^\circ,108^\circ,108^\circ,54^\circ$ ；安装凹凸后，所有新增角仍是  $18^\circ$  的整数倍。 $Q$  的角和平角也有这一性质。

因此，包含原顶点的会合点处满足

$$
120a+240b+18c=360,\qquad a+b>0,
$$

其中  $a,b,c$  为非负整数。取模得  $2a+b\equiv0\pmod3$ ，结合角度上界，只可能

$$
(a,b,c)=(3,0,0)\quad\text{或}\quad(1,1,0).
$$

所以原顶点只能与其他长条的原顶点会合。

选一块  $P$ ，将其恢复长条对齐一个六角网格。通过原顶点接触可达的全部长条，其方向和位置都属于同一网格。恢复这些长条后：

1. 若重叠一个六角格，其未修改的格心就同时处于两块  $P$  内部，矛盾。
2. 若占据格集合有一个边邻空格，公共边端点处的缺失扇形又必须由另一块通过原顶点可达的长条填上，矛盾。

占据格集合非空且对格邻接封闭；蜂窝网格连通，故覆盖整个平面。恢复长条既不重叠也不留空。双凸不可能出现，因此全部原边接触遵守  $R$ 。

合法修改留下的洞彼此隔离，每洞与  $Q$  全等。连通的填充块不能跨洞，每洞按面积恰需一块填充块。

## 6. 双向等价

给定遵守  $R$  的  $T$  平铺，替换成长条  $P$  并用  $Q$  填洞，即得平铺。反之，第 5 节从任意  $P,Q$  平铺恢复出遵守  $R$  的全平面长条平铺。因此

$$
\begin{aligned}
\mathrm{Tile}(P,Q)
&\Longleftrightarrow\mathrm{Tile}_R(T)\\
&\Longleftrightarrow\mathrm{Tile}(W(M))\\
&\Longleftrightarrow M\uparrow\\
&\Longleftrightarrow\mathrm{Con}(\mathrm{ZFC}).
\end{aligned}
$$

## 7. 代数坐标及边数

令

$$
h=\tan18^\circ,\qquad
5h^4-10h^2+1=0,\qquad \frac3{10}<h<\frac13.
$$

正五边形在缩放和居中前可用顶点

$$
(1,0),\ (\cos72^\circ,\sin72^\circ),\
(-\cos36^\circ,\sin36^\circ),\
(-\cos36^\circ,-\sin36^\circ),\
(\cos72^\circ,-\sin72^\circ)
$$

表示。由

$$
\cos36^\circ=\frac{1-h^2}{1+h^2},\qquad
\sin36^\circ=\frac{2h}{1+h^2}
$$

及二倍角公式，坐标属于  $\mathbb Q(h)$ 。截弦居中、镜像、有理尺度和位置仍保持该数域。六角格与  $60^\circ$  的整数倍旋转另需  $\sqrt3$ ，故

$$
\mathrm{Vertices}(P)\cup\mathrm{Vertices}(Q)
\subseteq\mathbb Q(h,\sqrt3).
$$

修改互不相交，故两者均为有限简单多边形。在本文分离的十二位置方案中，每条原边有十三段基线和三十六段半五边形轮廓，主多边形边数为

$$
49(4n+2).
$$

此公式只描述本文方案，不用于认证其他绘图或压缩版本。

## 8. 可证明性与核验范围

固定引用的有效归约后，有限编码和紧致性论证可在 ZFC 中形式化，得到

$$
\mathrm{ZFC}\vdash
\bigl(\mathrm{Tile}(P,Q)\leftrightarrow
\mathrm{Con}(\mathrm{ZFC})\bigr).
$$

“可形式化”不等于本文已经完成证明助手验证。

在元理论中假设 ZFC 一致，则所构造多边形实际能平铺，但 ZFC 不能证明它们能平铺，否则便证明了自身一致性，违反第二不完备定理。

仅凭一致性，不能进一步推出 ZFC 也不能证明“它们不能平铺”。保证双边独立的常用充分条件是 ZFC 的  $\Sigma_1$  可靠性；排除反面证明的精确条件为  $\mathrm{ZFC}+\mathrm{Con}(\mathrm{ZFC})$  一致。

原始示意图标注了 2,523,234,056,628,730,035,631 个六角形和 378,485,108,569,489,476,845,190 条边。**本文未核验这两个数值，也未确定图中省略的边界就是本文构造。** 认证该特定实例仍需完整的机器→Wang 瓦片→长条标签→边界坐标生成器及输出证书。

本文不主张证明了 ZFC 一致，也不作原创性、最优边数或最小机器状态数的主张。

## 参考文献

1. Jack Stade, *Two Tiling is Undecidable*, arXiv:2506.11628v1, 2025。引用第 2 节长条归约；原文第 3 节使用正十二边形，本文另给出上述正五边形和十二位置实现。[论文](https://arxiv.org/html/2506.11628v1)
2. Erik D. Demaine and Stefan Langerman, *Tiling with Three Polygons Is Undecidable*, SoCG 2025, LIPIcs 332, Article 39。引言说明非停机归约及 co-RE 难度。[论文](https://drops.dagstuhl.de/storage/00lipics/lipics-vol332-socg2025/html/LIPIcs.SoCG.2025.39/LIPIcs.SoCG.2025.39.html)
3. Raphael M. Robinson, *Undecidability and nonperiodicity for tilings of the plane*, Inventiones Mathematicae 12, 177–209, 1971。[DOI](https://doi.org/10.1007/BF01418780)
4. K215 固定发布版本，VladimirReshetnikov/ProveIt，提交 a61476422532a5d3b7dec11fc7a92751fe0d60f8。仅在选用特定 K215 时引用其校准。[发布说明](https://github.com/VladimirReshetnikov/ProveIt/blob/a61476422532a5d3b7dec11fc7a92751fe0d60f8/Computability/BusyBeaver/Research/ZFC/candidate-k215/README.md)
