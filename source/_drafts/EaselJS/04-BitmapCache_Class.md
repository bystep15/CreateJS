# BitmapCache Class

------

The BitmapCache is an internal representation of all the cache properties and logic required in order to "cache" an object. This information and functionality used to be located on a [cache](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache) method in [DisplayObject](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html), but was moved to its own class.

位图缓存表示了“缓存”一个对象所需的所有缓存属性和逻辑的内部表示。这些信息和功能过去通常位于[DisplayObject](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html)中的[缓存](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache)方法上，但在这里它被移到了自己的类中。

Caching in this context is purely visual, and will render the DisplayObject out into an image to be used instead of the object. The actual cache itself is still stored on the target with the [cacheCanvas](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#property_cacheCanvas). Working with a singular image like a [Bitmap](https://www.createjs.com/docs/easeljs/classes/Bitmap.html) there is little benefit to performing a cache as it is already a single image. Caching is best done on containers containing multiple complex parts that do not move often, so that rendering the image instead will improve overall rendering speed. A cached object will not visually update until explicitly told to do so with a call to update, much like a Stage. If a cache is being updated every frame it is likely not improving rendering performance. Cache are best used when updates will be sparse.

在这里讲的缓存是纯粹可视化的，并且将把DisplayObject渲染成用来代替对象的所需图像。实际的缓存本身仍然使用[cacheCanvas](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#property_cacheCanvas)存储在目标本身上。使用像[位图](https://www.createjs.com/docs/easeljs/classes/Bitmap.html)这样的单一图像，执行缓存几乎没有什么好处，因为它已经是单一的图像了。缓存最好用在包含多个不经常移动的复杂部分的容器上，以便可以更快的渲染图像，从而提高整体渲染速度。 一个缓存的对象不会直观地更新，除非通过调用更新来明确告诉它需要更新，这很像Stage。 如果缓存每帧更新一次，可能不会提高渲染性能。当很少更新时，最好使用缓存。

Caching is also a co-requisite for applying filters to prevent expensive filters running constantly without need, and to physically enable some effects. The BitmapCache is also responsible for applying filters to objects and reads each [Filte](https://www.createjs.com/docs/easeljs/classes/Filter.html)r due to this relationship. Real-time Filters are not recommended performance wise when dealing with a Context2D canvas. For best performance and to still allow for some visual effects use a compositeOperation when possible.

缓存也是使用过滤器的一个先决条件，以防止消耗过大的过滤器在不需要的情况下持续运行，并可以减少在物理上呈现的一些效果。由于这种关系，BitmapCache也负责将过滤器应用于对象并读取每个[过滤器](https://www.createjs.com/docs/easeljs/classes/Filter.html)。 处理Context2D画布时，不建议使用实时滤镜功能。为了获得最佳性能并且仍然允许使用一些视觉效果，请尽可能使用compositeOperation。

## Constructor

BitmapCache ()

## Methods:

- BitmapCache.cache (x, y, width, height, [scale=1], [options=undefined])

Actually create the correct cache surface and properties associated with it. Caching and it's benefits are discussed by the cache function and this class description. Here are the detailed specifics of how to use the options object.

实际上创建正确的缓存和与之相关的属性。 缓存和它的好处由缓存函数和这个类描述来决定。以下是如何使用选项对象的详细说明。

    - If options.useGL is set to "new" a StageGL is created and contained on this for use when rendering the cache.
    - If options.useGL is set to "stage" if the current stage is a StageGL it will be used. If not then it will default to "new".
    - If options.useGL is a StageGL instance it will not create one but use the one provided.
    - If options.useGL is undefined a Context 2D cache will be performed.

------
    
    - 如果options.useGL设置为“new”，则创建StageGL并将其渲染缓存时使用。
    - 如果options.useGL设置为“stage”，如果当前stage是StageGL，缓存会被使用。如果不是，那么它将默认为“new”。
    - 如果options.useGL是一个StageGL实例，它不会创建一个，而是使用提供的实例。
    - 如果options.useGL未定义，则使用2D内容缓存。

This means you can use any combination of StageGL and 2D with either, neither, or both the stage and cache being WebGL. Using "new" with a StageGL display list is highly unrecommended, but still an option. It should be avoided due to negative performance reasons and the Image loading limitation noted in the class complications above.

这意味着您可以将StageGL和2D的任意组合与stage和缓存作为WebGL一起使用。对StageGL显示列表使用“new”是非常不推荐的，但仍然是一种选择。 应该避免由于性能方面的负面原因以及上述提到的图像加载限制。

When "options.useGL" is set to the parent stage of the target and WebGL, performance is increased by using "RenderTextures" instead of canvas elements. These are internal Textures on the graphics card stored in the GPU. Because they are no longer canvases you cannot perform operations you could with a regular canvas. The benefit is that this avoids the slowdown of copying the texture back and forth from the GPU to a Canvas element. This means "stage" is the recommended option when available.

当“options.useGL”被设置为目标和WebGL的父级stage时，我们会通过使用“RenderTextures”而不是画布元素来提高性能。这些是存储在GPU中的图形上的内部纹理。因为他们不再是canvas，所以你不能用canvas的方法进行操作。这样做的好处是，可以避免将纹理从GPU复制到Canvas元素时的速度会减慢。这意味着“stage”可用时是推荐的选项。

A StageGL cache does not infer the ability to draw objects a StageGL cannot currently draw, i.e. do not use a WebGL context cache when caching a Shape, Text, etc.

StageGL缓存不会推断现在能不能绘制一个stageGL对象，例如，在缓存Shape，Text等时不使用WebGL上下文缓存。

WebGL cache with a 2D context

```
var stage = new createjs.Stage();
var bmp = new createjs.Bitmap(src);
bmp.cache(0, 0, bmp.width, bmp.height, 1, {gl: "new"});          // no StageGL to use, so make one

var shape = new createjs.Shape();
shape.graphics.clear().fill("red").drawRect(0,0,20,20);
shape.cache(0, 0, 20, 20, 1);                             // cannot use WebGL cache
```

WebGL cache with a WebGL context

```
var stageGL = new createjs.StageGL();
var bmp = new createjs.Bitmap(src);
bmp.cache(0, 0, bmp.width, bmp.height, 1, {gl: "stage"});       // use our StageGL to cache

var shape = new createjs.Shape();
shape.graphics.clear().fill("red").drawRect(0,0,20,20);
shape.cache(0, 0, 20, 20, 1);                             // cannot use WebGL cache
```

You may wish to create your own StageGL instance to control factors like clear color, transparency, AA, and others. If you do, pass a new instance in instead of "true", the library will automatically set the StageGL/isCacheControlled to true on your instance. This will trigger it to behave correctly, and not assume your main context is WebGL.

您可能希望创建自己的StageGL实例来控制诸如颜色的清晰度，透明度，AA和其他因素。如果你这样做，请传入一个新的实例而不是“true”，库会自动将StageGL / isCacheControlled设置为true。 这将触发它的正确行为，并且不会假定您的主要上下文是WebGL。

Parameters:
    - x:The x coordinate origin for the cache region.(缓存区域的x坐标原点。)
    - y:The y coordinate origin for the cache region.(缓存区域的y坐标原点。)
    - width:The width of the cache region.(缓存区域的宽度)
    - height:The height of the cache region.(缓存区域的高度)
    - [scale=1]:The scale at which the cache will be created. For example, if you cache a vector shape using myShape.cache(0,0,100,100,2) then the resulting cacheCanvas will be 200x200 px. This lets you scale and rotate cached elements with greater fidelity. Default is 1.(缓存创建的规模。例如，如果使用myShape.cache（0,0,100,100,2）缓存矢量形状，则生成的cacheCanvas将为200x200像素。 这可让您以更高的保真度缩放和旋转缓存的元素。 缺省值是1。)
    - [options=undefined]:Specify additional parameters for the cache logic(缓存逻辑的额外参数)
    - [useGL=undefined] Undefined | "new" | "stage" | StageGL:Select whether to use context 2D, or WebGL rendering, and whether to make a new stage instance or use an existing one. See above for extensive details on use.(选择是否使用2D内容或者webGL渲染，或者是使用新得stage对象还是使用已存的一个。请在使用时查看额外的细节。)

- draw (ctx)

Use context2D drawing commands to display the cache canvas being used.

使用2D内容绘制指令展示正在使用的缓存canvas

Parameters:

    - ctx:The context to draw into(要绘制的内容)

Returns:
    
Whether the draw was handled successfully.(返回绘制是否成功)

- getCacheDataURL()

Returns a data URL for the cache, or null if this display object is not cached. Uses cacheID to ensure a new data URL is not generated if the cache has not changed.

返回缓存数据的URL，如果要展示的对象没有缓存，则返回null。使用cacheID可以确保如果缓存没有变化时，不会生成新的数据URL。

Returns:
  
The image data url for the cache.(缓存图像的数据URL)

- getFilterBounds(target, [output=null])

Returns the bounds that surround all applied filters, relies on each filter to describe how it changes bounds.

返回所有应用过滤器周围的边界，依靠每个过滤器来描述它如何改变边界。

Parameters:

    - target:The object to check the filter bounds for.(检查过滤器边界的对象。)
    - [output=null]:Optional parameter, if provided then calculated bounds will be applied to that object.(可选参数，如果提供参数，则计算将会被应用到的对象的边界)

Returns:

     bounds object representing the bounds with filters.(边界对象表示带有滤镜的边界。)

- release()

Reset and release all the properties and memory associated with this cache.

重置并释放所有与缓存相关的属性和记录

- toString ()

Returns a string representation of this object.

返回这个对象的字符串表达式

Returns:

 a string representation of the instance.

 这个对象的字符串表达式

- update ([compositeOperation=null])

Directly called via [updateCache](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_updateCache), but also internally. This has the dual responsibility of making sure the surface is ready to be drawn to, and performing the draw. For full details of each behaviour, check the protected functions [\_updateSurface](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html#method__updateSurface) and [\_drawToCache](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html#method__drawToCache) respectively.

直接通过[updateCache](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_updateCache)调用，但也可以在内部调用。这个操作有两个作用，确保画布表面准备好被绘制，并执行绘制。有关每种行为的完整详细信息，请分别检查受保护的函数[\_updateSurface](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html#method__updateSurface)和[\_drawToCache](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html#method__drawToCache)。

Parameters:

    [compositeOperation=null]:The DisplayObject this cache is linked to.(与缓存相关联的DisplayObject)

