# 变换

## 向量

### 基本概念

点坐标：$ P=(x,y,z,1)^T $

线坐标：$ \vec V=(x,y,z,0)^T $

### 基本运算

向量长度：

$ ||\vec V||=\sqrt{x^2+y^2+z^2} $

向量加减：

$ \vec V_2-\vec V_1 = (x_2-x_1,y_2-y_1,z_2-z_1)^T $

向量点乘：

$ \vec V_1 \cdot \vec V_2=x_1x_2+y_1y_2+z_1z_2 $

向量点乘几何意义：一向量在另一向量上的投影长度

$ \vec V_1 \cdot \vec V_2=||\vec V_1||\cdot||\vec V_2||\cos (\theta) $

向量叉乘（只讨论正交） ：法向量

$ \vec V_1 \times \vec V_2= 
 \begin{bmatrix}
   y_1z_2-y_2z_1  \\\
   z_1x_2-z_2x_1  \\\
   x_1y_2-x_2y_1 
  \end{bmatrix}
$

## 坐标变换

### 缩放

定义缩放矩阵：
$ K = 
 \begin{bmatrix}
   k_x & 0 & 0 & 0\\\
   0 & k_y & 0 & 0\\\
   0 & 0 & k_z & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

则缩放后的向量为：
$ K \vec V=
 \begin{bmatrix}
   k_xx & 0 & 0 & 0\\\
   0 & k_yy & 0 & 0\\\
   0 & 0 & k_zz & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

### 位移

定义平移矩阵：
$ T = 
 \begin{bmatrix}
   1 & 0 & 0 & T_x\\\
   0 & 1 & 0 & T_y\\\
   0 & 0 & 1 & T_z\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

则平移后的向量为：
$ T \vec V=
 \begin{bmatrix}
   x+T_x & 0 & 0 & 0\\\
   0 & y+T_y & 0 & 0\\\
   0 & 0 & z+T_z & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

### 旋转

旋转分为沿x轴、y轴、z轴旋转：

沿x轴旋转的旋转矩阵为：
$ R_x = 
 \begin{bmatrix}
   1 & 0 & 0 & 0\\\
   0 & \cos \theta & -\sin \theta & 0\\\
   0 & \sin \theta & \cos \theta & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

沿y轴旋转的旋转矩阵为：
$ R_y = 
 \begin{bmatrix}
   \cos \theta & 0 & \sin \theta & 0\\\
   0 & 1 & 0 & 0\\\
   -\sin \theta & 0 & \cos \theta & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$

沿z轴旋转的旋转矩阵为：
$ R_z = 
 \begin{bmatrix}
   \cos \theta & -\sin \theta & 0 & 0\\\
   \sin \theta & \cos \theta & 0 & 0\\\
   0 & 0 & 1 & 0\\\
   0 & 0 & 0 & 1
  \end{bmatrix}
$