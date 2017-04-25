# Align

Align 函数帮助你迅速地把一个元素在屏幕中相对于它的父级摆放好位置。使用它们把一个层放置在它的父级的上下左右或中间。它可以作为层属性用在状态或者动画中。

```coffeescript
    # Create a layer an position it in the center 
    layerA = new Layer
        x: Align.center
        y: Align.center
     
    # Create a state in the bottom right corner 
    layerA.states.add
        a:
            x: Align.right
            y: Align.bottom
        b:
            x: Align.left
            y: Align.top

    layerA.onTap -> layerA.states.next()
```

当你需要某个元素的坐标值的时候，Align 函数可以动态地计算出它的坐标值。例如有一个情况是把一个层放在右下角，Align 函数就可以做到，即使你在转换状态时调整屏幕尺寸。

你也可以选择性地使用偏移量。

```coffeescript
	layerA = new Layer
	    x: Align.center(-100) # 100 pixels left from the center 
	    y: Align.top(100) # 100 pixels from the top 
```

需要注意的是 left 和 right 只对 x 值起作用，top 和 bottom 只对 y 值起作用，center 对他们都起作用。在直接编程时，对比于 layer.center() Align 更加灵活，因为它可以自适应。

<a id="align.bottom"></a>
## align.bottom(offset)

把层置于它的父级的底部。如果没有父级，就放在设备屏幕底部。Bottom 只对层的 y 属性起作用，它可以作用在属性、状态及动画中。

### 参数

* **offset** — 数字(可选的)

```coffeescript
    layerA = new Layer
        y: Align.bottom
     
    layerB = new Layer
        y: Align.bottom(-100) # 100 pixels from the bottom 
```

<a id="align.center"></a>
## align.center(offset)

该方法可以把层放在它的父层的正中间。如果没有父层，就默认放在屏幕正中间。在使用状态和动画的时候，它也可以作为一个属性值去使用。

### 参数

* **offset** — 数字(可选的).

```coffeescript
    layerA = new Layer
        x: Align.center
        y: Align.center
     
    layerB = new Layer
        x: Align.center(+100)
        y: Align.center(-100)
```

<a id="align.left"></a>
## align.left(offset)


把层置于它的父层的左侧，如果没有父层，就默认放在屏幕左侧。这个方法只对 x 属性起作用。它也可以作为状态或者动画中的一个属性值。

### 参数

* **offset** — 数字(可选的).


    layerA = new Layer
        x: Align.left
     
    layerB = new Layer
        x: Align.left(100) # 100 pixels from the left 

<a id="align.right"></a>
## align.right(offset)

把层置于它的父层的右侧，如果没有父层，就默认放在屏幕右侧。这个方法只对x属性起作用。它也可以作为状态或者动画中的一个属性值。

### 参数

* **offset** — 数字(可选的).


    layerA = new Layer
        x: Align.right
     
    layerB = new Layer
        x: Align.right(-100) # 100 pixels from the right 

<a id="align.top"></a>
## align.top(offset)

把层置于它的父层的顶部，如果没有父层，就默认放在屏幕顶部。这个方法只对 y 属性起作用。它也可以作为状态或者动画中的一个属性值。

### 参数

* **offset** — 数字(可选的).


    layerA = new Layer
        y: Align.top
     
    layerB = new Layer
        y: Align.top(100) # 100 pixels from the top 
