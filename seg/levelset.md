# LevelSet/水平集

## 背景

分割类的算法有很多种，这个水平集算法的想法可以说是很有特点。它将画面的分割问题以一种动态的形式来表现。

## 水平集

什么是水平集？我们有一个图片I(y,x),其中y,x代表其横纵坐标。每一个点上都有一个值，一般来说我们指这个值是图像在这一个像素的颜色值。

当然，我们也可以在这些点上定义其他的信息，比方说梯度，每一个点都可以算出它的梯度，有横轴梯度，也有纵轴梯度。

如果我们在图片的这些点上定义一个函数，如ƒ(y,x),那么我们可以求出ƒ(y,x)=c的所有点，而这些点就构成了一个水平集，表示它们在同一水平上。

水平集还有什么方便理解的方式呢？我们常见的一种类似水平集的东西叫做等高线。等高线是一段具有相同高度的线段，在地形图上可以表示相同海拔，在一些数值优化问题中，它可以表示相等数值的区域。

## 水平集的移动

我们知道在优化问题中，一个优化点会随着梯度等信息不断下降，最终到达最优点。水平集上的这些点同样具有这个特性，它们也会受到一些外力的作用，改变它们所在的位置，朝着其他的位置移动。


## 水平集的两种状态公式

### 边界值公式

我们假设一些初始的点位置，令T(x,y)表示从初始位置开始，某种作用力作用于这些点，使这些点开始移动，到达(x,y)时的时刻。T(1)表示t=1时的点集，S(2)表示t=2时的点集，以此类推。

我们令F为受到的外力，可以定义这样一个公式：

```python
abs(delta(T)) * F = 1
given T(0)
```

其中delta(T)表示一个点的移动轨迹上移动一小段距离所花费的时间，这个公式表明移动距离和受到的力呈现反相关，力越大，时间越短。

这个方程和经典的Eikonal方程相近。

### 初始值公式

上面的算法根据达到时间进行建模，下面的算法则根据另一种方式。我们假设有一个函数phi，这个函数等于0的点为当前选定的一些点，随着时间的推移，力不断作用于这些点上，这些点会随之移动，而这个函数phi也会变动，以保证新选定的点依然是phi=0的点。我们令x(t)表示t时刻的点的坐标，那么有
```python
phi(x(t),t) = 0 # 根据链式法则
∂phi/∂t + ∂phi/∂x * ∂x/∂t = 0
=> ∂phi/∂t + delta(phi) * ∂x/∂t = 0

# 由于力的方向与当前点的切线方向垂直，所以∂x/∂t * n = F
# n = delta(phi) / abs(delta(phi))
=> ∂phi/∂t + F * abs(phi) = 0
given phi(x, t=0)
```

这个方程满足经典的Hamilton-Jacobi等式。

## 初始值公式的展开

### F的解法

### phi的更新 