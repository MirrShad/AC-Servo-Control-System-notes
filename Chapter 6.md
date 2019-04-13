# 第六章 永磁同步电动机控制技术
## 6.1 永磁同步电动控制原理
永磁同步电动机的转子按永磁体结构可以分为
- 表面式永磁同步电动机，属于隐极式
永磁体粘结到转子铁心表面，估计是容易磨损，适用于转子转速低  
有效气隙[1]较大，同步电抗小[2]，电枢反应小  
气隙均匀，即$X_d = X_q$  
- 内置式永磁同步电动机，属于凸极式  
永磁体镶嵌在转子铁心内部，适用于高速运行场合  
有效气隙较小，d轴和q轴的同步电抗较大，电枢反应磁动势较大，从而存在较大的弱磁空间  
  
下面是我们要控制的定子绕组的情况。相数=3，槽数=36，极对数=4，极距=9，每极每相=3，节距=8。[3]和无刷直流电机电动绕组的区别在于采用短距绕组方式和分布绕组方式，来让绕组感应反电动势尽量为正弦波

### 6.1.1 永磁同步电动机的数学模型
列了五条理想化条件，最重要的是电机属于隐极式，我们不考虑另一种电动机
1. 静止坐标系OABC下的数学模型
我对物理没有太大的兴趣，这里一个个公式的推导我没有仔细看，所以直接列结论了
$$
\begin{pmatrix}u_A\\u_B\\u_C\\\end{pmatrix} = \begin{pmatrix}{R_s+Lp\qquad 0\qquad 0}\\{0\qquad R_s+Lp \qquad 0}\\{0\qquad 0 \qquad R_s+Lp}\\\end{pmatrix}\begin{pmatrix}i_A\\i_B\\i_C\\\end{pmatrix}-\psi_f \omega_r \begin{pmatrix}sin\theta\\sin(\theta-120)\\sin(\theta-240)\\\end{pmatrix}
$$
式中，$u_A \ u_B \ u_C$是各相定子绕组相电压，$i_A \ i_B \ i_C$是各相定子绕组相电流，$R_s$是电枢绕组电阻，p是微分算子d/dt，
2. $O\alpha\beta$轴系下的数学模型（3/2变换 Clarke变换）  
把
$$
\begin{pmatrix}u_\alpha\\u_\beta\\\end{pmatrix}=\sqrt{\frac{2}{3}}\begin{pmatrix}{1 \qquad -\frac{1}{2} \qquad -\frac{1}{2}}\\{0 \qquad \frac{\sqrt{3}}{2} \qquad -\frac{\sqrt{3}}{2}}\\\end{pmatrix}\begin{pmatrix}u_A\\u_B\\u_C\\\end{pmatrix} 
$$
$$
\begin{pmatrix}i_\alpha\\i_\beta\\\end{pmatrix}=\sqrt{\frac{2}{3}}\begin{pmatrix}{1 \qquad -\frac{1}{2} \qquad -\frac{1}{2}}\\{0 \qquad \frac{\sqrt{3}}{2} \qquad -\frac{\sqrt{3}}{2}}\\\end{pmatrix}\begin{pmatrix}i_A\\i_B\\i_C\\\end{pmatrix} 
$$
带入上式
3. $Odq$轴系下的数学模型（旋转变换 Park变换）  
$$
\begin{pmatrix}u_d\\u_q\\\end{pmatrix} = \begin{pmatrix}{cos\theta \qquad sin\theta}\\{-sin\theta \qquad cos\theta}\\\end{pmatrix}\begin{pmatrix}u_\alpha\\u_\beta\\\end{pmatrix}
$$
$$
\begin{pmatrix}i_d\\i_q\\\end{pmatrix} = \begin{pmatrix}{cos\theta \qquad sin\theta}\\{-sin\theta \qquad cos\theta}\\\end{pmatrix}\begin{pmatrix}i_\alpha\\i_\beta\\\end{pmatrix}
$$
___
<font size="2">
附录[1]:电机气隙指的是静止的磁极和旋转的电枢之间的间隙。气隙的大小，决定磁通量的大小，如果气隙较大的话，漏磁就多，那么电机的效率就会降低，如果气隙太小，就容易扫定子膛。因此，需要将气隙控制到一个合理的数值，才能达到最佳效果。小容量电机中，气隙为0.5~3mm。这里有效气隙较大，应该是指因为永磁体贴在表面所以和电枢间隙小，所以气隙较小，漏磁比较少，利用效率高  
</font><br /> 
<font size="2">
附录[2]:同步电抗是同步电机的定子漏抗与电枢反应电抗之和  
</font><br /> 
<font size="2">
附录[3]:
</font><br />
![定子参数介绍](https://github.com/MirrShad/AC-Servo-Contorl-System-notes/blob/master/Images/Chapter6/%E7%94%B5%E6%9C%BA%E6%9E%81%E6%95%B0%E7%9B%B8%E6%95%B0%E5%85%B3%E7%B3%BB%E5%9B%BE.jpg)