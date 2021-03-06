# Extras

`Extras`是Framer额外的一些功能，如果你有一些特殊的诸如预加载、触摸仿真和提示的需求可以使用它。
>Extras are optional parts of Framer that have specific tasks like preloading, touch emulation and hints. In general, they are enabled automatically based on where your prototype is shown. But extras are often overridable explicitly by you, if you require specific behaviour.

<a id="extras.Hints"></a>
## Hints

`Hints`用来提示用户哪些地方是可交互区域，比如点击、滑动等，这可以在用户第一回看见这个原型时指导他们如何使用。
>Hints are used to highlight layers that a user can interact with, such as taps, swipes, etc. They are mainly to help users discover what a project can do when they see it for the first time.

默认情况下，`Hints`在你使用Framer软件和分享到web时都会启用。如果你点击了可交互区域之外，那么原型中就会有紫色的框来提示你哪里可以点击或者滑动。
>By default, hints are enabled both in Framer for Mac and when you share your prototypes with others. If you click anywhere outside of an interactive layer or outside of the device, purple rectangles will indicate the tappable or scrollable areas.

你可以像这样启用或者禁用提示。
>You can enable or disable hints for your entire projects like this:

    Framer.Extras.Hints.disable()

或者像这样启用：
>Or enable them like this:

    Framer.Extras.Hints.enable()

如果你想在原型加载完毕之前立即显示点击区域提示，而不需要用户点击才触发，你可以这样写：
>If you would like to show hints directly after a page loads, without any clicks you can do this:

    Framer.Extras.Hints.enable()
    Framer.Extras.Hints.showHints()

### 一些注意事项:

1. 当你点击（不拖着滚动）一个可拖拽或可滑动图层时它会被高亮显示。
2. 只有当可拖拽或可滑动图层确实可以水平或垂直滑动时才会有高亮提示。
3. 有圆角的图层的提示框也是有圆角的。
4. 旋转的图层现在还不支持提示。
5. 不可见图层不会显示提示框，除非它们是被你设置为不可见或者透明度为0的。如果它们被其它图层覆盖但是任然可以响应触摸事件，他们还是会有提示框。

>Draggable or scrollable areas will highlight if you tap them, but did not scroll.<br>
Draggable or scrollable areas will only highlight if they can either scroll horizontal or vertically.<br>
Layers with rounded corners will get a hint with rounded corners.<br>
Rotated layers are currently unsupported.<br>
Invisible layers will not show hints, unless they are set to invisible or their opacity is 0. They will show a hint if they are covered by another layer but still respond to taps.

### 定制

你可以覆盖一些图层（也包括基于图层的组件）的定义，去定制特殊样式的提示框（默认是紫色的方形框）。当你不想让一些图层显示提示框，或者想自己定义特别的提示框样式时，这将会很好用。
>You can override layers (or components based on layers) to customize the hint indicator (by default a purple rectangle). This is great when you want to disable the highlight on a specific layer, or have a specific visiual hint.

下面代码展示的是如何在一些特殊图层上禁用提示框。
>This is how you disable a hint on a specific layer:

    layerA = new Layer
    layerA.onTap -> print "layerA"
     
    layerB = new Layer x: 220
    layerB.onTap -> print "layerB"
 
    # Set an empty function on showHint 
    # 将showHint设为空函数
    layerB.showHint = -> print "nope"

你可以像这样自己定制提示框样式。
>And you can customize the hint the same way:

    layerA = new Layer
    layerA.onTap -> print "layerA"
     
    layerB = new Layer x: 220
    layerB.onTap -> print "layerB"
     
    layerB.showHint = (hintFrame) ->
 
        # Create a hint layer, this will automatically be   
        # placed in the hints context on top of everything. 
        # 创建一个提示图层，他将会被自动放置到提示框所处的层级，在所有图层上面。
        hint = new Layer
            frame: hintFrame
            backgroundColor: "red"
            opacity: 0.5
     
        # Add a cool animation 
        # 添加一个酷酷的显示动画
        hint.animate
            properties:
                scale: 1.3
                opacity: 0
            time: 0.5
     
        # Remove the layer when done 
        # 动画显示出来之后移除它们
        hint.onAnimationEnd -> hint.destroy()

<a id="extras.Preloader"></a>
## Preloader

当你打开一个项目，我们的预加载器`preloader`会确保所有媒体资源都会在完全显示你的项目原型之前被加载完毕。他将会分析你的图片或视频资源并且在后台加载，而在页面上显示一个环形进度条来表明加载进度。当所有资源加载完毕时它会展示你的项目文件。
>When you open a project, our preloader makes sure your media is loaded before fully displaying. It analyzes the images and video you use and downloads them in the background, all while showing a circular progress indicator. When everything is fully loaded, it displays your project simultaneously.

预加载进度条可以极大地提高用户体验，因为它不会让用户看见你项目未完全加载的状态。当用户在你的原型还未加载完全时就进行操作，可能会出现一些奇怪的事情，因为此时图片也在解压变化。
>A preloader vastly improves the user's experience because it avoids displaying your project in an incomplete state. When users interact with a prototype that is still loading, performance can suffer due to images being decompressed on the same thread that handles user interaction.

默认情况下`preloader`只会在 Framer 软件以外可以用，比如分享到网络的原型或正在镜像展示的原型。
>By default the preloader is only enabled outside of Framer, such as when you share a project online or via mirroring.

你可以强制开启`preloader`：
>You can force enable the preloader like this:

    Framer.Extras.Preloader.enable()

或者禁用：
>Or disable it like this:

    Framer.Extras.Preloader.disable()

### 定制

>You can customize the preloader image with any image, such as your logo. To do so, use the setLogo() function:

    Framer.Extras.Preloader.enable()
    Framer.Extras.Preloader.setLogo("https://twitter.com/framerjs/profile_image?size=bigger")

### 手动改变加载状态图片

>While the preloader often does a great job of discovering the main images used in your project, it may fail to locate specific images that were used at arbitrary points. The preloader also allows you to add these images manually using Framer.Extras.Preloader.addImage().

>In the example below, the preloader cannot discover the image that layerB uses because it only gets created after a tap, and theoretically could be any url. So in this scenarios, we add the image manually at the top of the prototype.

    Framer.Extras.Preloader.enable()
    Framer.Extras.Preloader.addImage("https://twitter.com/framerjs/profile_image?size=bigger")
     
    layerA = new Layer point: Align.center
     
    layerA.onTap ->
        layerB = new Layer
            image: "https://twitter.com/framerjs/profile_image?size=bigger"

### 一些注意事项:


>Device images are not counted against the preloader and are shown instantly because they are likely cached.
There is a 30 second hard timeout on the preloader, after which your project gets shown even if not all images are loaded.
Cached images load faster the second time you visit a project.
Video preloading is based on the canplay event when enough buffer is available to play them.
Loading errors are counted as loaded, so that the project appears even if some images are missing.
The progress is based on image count and not loaded bytes, so if you have many small images and one big one, the last step may be significantly longer. Unfortunately, there is no great way to get progress based on size today.
