# BitMap

------

A Bitmap represents an Image, Canvas, or Video in the display list. A Bitmap can be instantiated using an existing HTML element, or a string.

位图表示显示列表中的图像，画布或展式列表中的视频。位图可以使用现有的HTML元素或字符串来实例化。

Example:
```
var bitmap = new createjs.Bitmap("imagePath.jpg");
```
Notes(说明):

1. When using a video source that may loop or seek, use a [VideoBuffer](https://www.createjs.com/docs/easeljs/classes/VideoBuffer.html) object to prevent blinking / flashing.

2. When a string path or image tag that is not yet loaded is used, the stage may need to be redrawn before it will be displayed.

3. Bitmaps with an SVG source currently will not respect an alpha value other than 0 or 1. To get around this, the Bitmap can be cached.

4. Bitmaps with an SVG source will taint the canvas with cross-origin data, which prevents interactivity. This happens in all browsers except recent Firefox builds.

5. Images loaded cross-origin will throw cross-origin security errors when interacted with using a mouse, using methods such as getObjectUnderPoint, or using filters, or caching. You can get around this by setting crossOrigin flags on your images before passing them to EaselJS, eg: img.crossOrigin="Anonymous";

---

1. 当想要的视频源可以循环或者指定时间播放时，使用[VideoBuffer](https://www.createjs.com/docs/easeljs/classes/VideoBuffer.html)对象阻止闪烁。

2. 当字符串路径或者图片标签的图片在还没加载完就使用时，舞台也许会在它展示之前重新绘制。

3. 使用SVG源的位图当前不会考虑除0或1以外的alpha值。要解决此问题，可以缓存位图。

4. 带有SVG源的位图如果使用跨域的数据可能会污染画布，从而妨碍交互性。 这种情况ui发生在除最近的Firefox版本之外的所有浏览器中。

5. 对于带有跨域源的图片来说，当使用鼠标交互或者使用诸如getObjectUnderPoint之类的方法，或者使用过滤器或缓存时，会抛出跨域的安全问题。您可以通过在你的图像上设置crossOrigin标签，将它们传递给EaselJS来解决这个问题。

## Constructor(构造函数):

Bitmap ( imageOrUri )

Parameters(参数):

imageOrUri CanvasImageSource | String | Object

The source image to display. This can be a CanvasImageSource (image, video, canvas), an object with a getImage method that returns a CanvasImageSource, or a string URL to an image. If the latter, a new Image instance with the URL as its src will be used.

要展示的源图片。可以是一个CanvasImageSource(例如图片，视频，canvas)，也可以是一个带有getImage方法，并返回一个CanvasImageSource的对象，也可以是一个图片的字符串URL。如果是后者，一个将此URL作为地址的新的图片实例将会被创建。

## Methods(方法):

- \_updateState ()

Called before the object gets drawn and is a chance to ensure the display state of the object is correct. Mostly used by [MovieClip](https://www.createjs.com/docs/easeljs/classes/MovieClip.html) and [BitmapText](https://www.createjs.com/docs/easeljs/classes/BitmapText.html) to correct their internal state and children prior to being drawn.

在对象被绘制之前调用，并且可以保证展示对象状态的正确性。大多数使用[MovieClip](https://www.createjs.com/docs/easeljs/classes/MovieClip.html)和[BitmapText](https://www.createjs.com/docs/easeljs/classes/BitmapText.html)来确保其内部状态和它的子元素可以优先被渲染。

Is manually called via draw in a [Stage](https://www.createjs.com/docs/easeljs/classes/Stage.html) but is automatically called when present in a [StageGL](https://www.createjs.com/docs/easeljs/classes/Stage.html) instance.

此方法在[Stage](https://www.createjs.com/docs/easeljs/classes/Stage.html)中手动调用，但在[StageGL](https://www.createjs.com/docs/easeljs/classes/Stage.html)实例中自动调用。

- addEventListener (type, listener, [useCapture] )

Adds the specified event listener. Note that adding multiple listeners to the same function will result in multiple callbacks getting fired.

添加特殊的事件监听器。注意，当使用同一个方法监听多个监听器时，会导致多个回调失效。

example(例子):

```
displayObject.addEventListener("click", handleClick);
function handleClick(event) {
    // Click happened.
 }
```

Parameters(参数):

    - type:The string type of the event.(事件类型)
    - listener:An object with a handleEvent method, or a function that will be called when the event is dispatched.(一个带有处理事件方法的对象，或者在事件被触发时被调用)
    - [useCapture]:For events that bubble, indicates whether to listen for the event in the capture or bubbling/target phase.(用于事件冒泡，指示是否在捕获或冒泡/目标阶段监听事件。)

Returns:
    Returns the listener for chaining or assignment.(返回链接或者分配的监听器)

- cache():

Because the content of a Bitmap is already in a simple format, cache is unnecessary for Bitmap instances. You should not cache Bitmap instances as it can degrade performance.

因为位图的内容已经是一种简单的格式，因此对于位图实例并不需要缓存。所以您不应该缓存位图实例，因为它可能会降低性能。

However: If you want to use a filter on a Bitmap, you MUST cache it, or it will not work. To see the API for caching, please visit the DisplayObject [cache](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache) method.

但是：如果您想在位图上使用过滤器，您必须缓存它，否则过滤器不会生效。请看缓存的API，查看DisplayObject[缓存](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache)的方法。

- clone(node)

Returns a clone of the Bitmap instance.

返回克隆的位图实例。

Parameters(参数)：
    node：Whether the underlying dom element should be cloned as well.(决定底层dom元素是否也应该被克隆。)

Returns:

    Bitmap: a clone of the Bitmap instance.(返回一个克隆的位图实例)

- dispatchEvent(eventObj, [bubbles], [cancelable])

Dispatches the specified event to all listeners.

将指定的事件分派给所有监听器。

Example：
```
// Use a string event
this.dispatchEvent("complete");

// Use an Event instance
var event = new createjs.Event("progress");
this.dispatchEvent(event);
```

Parameters:
    
    - eventObj:An object with a "type" property, or a string type. While a generic object will work, it is recommended to use a CreateJS Event instance. If a string is used, dispatchEvent will construct an Event instance if necessary with the specified type. This latter approach can be used to avoid event object instantiation for non-bubbling events that may not have any listeners.(具有“type”属性或字符串类型的对象。 尽管使用通用对象也能达到一样的效果，但还是建议使用CreateJS Event实例。如果使用字符串，则dispatchEvent将根据需要构造一个Event实例并使用指定的类型。 后一种方法可用于避免可能没有任何侦听器的非冒泡事件的事件对象实例化。)

    - [bubbles]  (optional):Specifies the bubbles value when a string was passed to eventObj(指定字符串传递给eventObj时的bubbles值)

    - [cancelable]  (optional):Specifies the cancelable value when a string was passed to eventObj.(指定字符串传递给eventObj时的cancelable值)

- draw (ctx, [ignoreCache=false])

Draws the display object into the specified context ignoring its visible, alpha, shadow, and transform. Returns true if the draw was handled (useful for overriding functionality).

将显示对象绘制到指定的上下文中，会忽略其可见性，alpha值，阴影和变换类型。如果绘图已处理，则返回true（用于重写功能）。

NOTE: This method is mainly for internal use, though it may be useful for advanced uses.

此方法主要用于内部使用，尽管它可以被用作更加高级的使用。

Parameters:

    - ctx:The canvas 2D context object to draw into.(绘制2D内容的canvas对象)
    - [ignoreCache=false]:Indicates whether the draw operation should ignore any current cache. For example, used for drawing the cache (to prevent it from simply drawing an existing cache back into itself).(指示绘制操作是否应该忽略当前的任何缓存。例如，用于绘制缓存(以防止它使用地现有的缓存)。)

Returns: Boolean

- getBounds ()

Returns a rectangle representing this object's bounds in its local coordinate system (ie. with no transformation). Objects that have been cached will return the bounds of the cache.

返回一个代表该对象在其本地坐标系中的边界的矩形（即不带转换）。 已缓存的对象将返回缓存的边界。

Not all display objects can calculate their own bounds (ex. Shape). For these objects, you can use setBounds so that they are included when calculating Container bounds.

并非所有显示对象都可以计算它们自己的边界（例如形状）。 对于这些对象，可以使用setBounds，以便在计算容器边界时包含它们。

    1. All:All display objects support setting bounds manually using setBounds(). Likewise, display objects that have been cached using cache() will return the bounds of their cache. Manual and cache bounds will override the automatic calculations listed below.
    2. Bitmap:Returns the width and height of the sourceRect (if specified) or image, extending from (x=0,y=0).
    3. Sprite:Returns the bounds of the current frame. May have non-zero x/y if a frame registration point was specified in the spritesheet data. See also [getFrameBounds](https://www.createjs.com/docs/easeljs/classes/SpriteSheet.html#method_getFrameBounds)
    4. Container:Returns the aggregate (combined) bounds of all children that return a non-null value from getBounds().
    5. Shape:Does not currently support automatic bounds calculations. Use setBounds() to manually define bounds.
    6. Text:Returns approximate bounds. Horizontal values (x/width) are quite accurate, but vertical values (y/height) are not, especially when using textBaseline values other than "top".
    7. BitmapText:Returns approximate bounds. Values will be more accurate if spritesheet frame registration points are close to (x=0,y=0).

---
    
    1. 所有元素：所有显示对象都支持使用setBounds()手动设置边界内容。同样，使用cache()缓存的显示对象将返回缓存的边界。手动和缓存边界将覆盖下面列出的内容
    2. 位图：从x=0,y=0的位置返回源矩形（如果指定）或者图片的宽度或者高度
    3. 精灵：返回当前帧的边界。如果在spritesheet数据中指定了帧的位置，则可能具有非零的x / y。另请参阅[getFrameBounds](https://www.createjs.com/docs/easeljs/classes/SpriteSheet.html#method_getFrameBounds)
    4. 容器：返回所有从getBounds（）中返回的非空值的子组合边界
    5. 形状：当前不支持自动计算边界。可以使用setBounds（）手动定义边界
    6. 文本：返回大致的边界。水平值（x / width）非常准确，但垂直值（y / height）并不是，特别是在使用除“top”之外的textBaseline值的时候。
    7. 位图文本：返回大致的边界。如果spritesheet的帧接近（x = 0，y = 0）时，值将更加精确。

Bounds can be expensive to calculate for some objects (ex. text, or containers with many children), and are recalculated each time you call getBounds(). You can prevent recalculation on static objects by setting the bounds explicitly:

对于某些对象（例如文本或含有许多子项的容器来说）计算边界可能很复杂，并且每次调用getBounds（）时都会重新计算边界。您可以通过显式设置边界来防止重新计算静态对象的属性：

```
var bounds = obj.getBounds();
obj.setBounds(bounds.x, bounds.y, bounds.width, bounds.height);
// getBounds will now use the set values, instead of recalculating
```

To reduce memory impact, the returned Rectangle instance may be reused internally; clone the instance or copy its values if you need to retain it.

为了减少缓存的影响，返回的矩形实例也会会在内部被重用；如果您需要保留它时，您可以克隆这个实例或者拷贝它的值。

```
var myBounds = obj.getBounds().clone();
// OR:
myRect.copy(obj.getBounds());
```

Returns: A Rectangle instance representing the bounds, or null if bounds are not available for this object.(一个代表边界的矩形实例，如果边界无效，则返回null)

- getCacheDataURL()

Returns a data URL for the cache, or null if this display object is not cached. Only generated if the cache has changed, otherwise returns last result.

返回缓存的数据URL，如果该展示的元素没有被缓存时，返回null。只有在缓存改变的时候才会生成该值。否则返回最后一个值。

Returns:The image data url for the cache.(缓存图片的数据地址)

getConcatenatedDisplayProps ([props])

Generates a DisplayProps object representing the combined display properties of the object and all of its parent Containers up to the highest level ancestor (usually the [Stage](https://www.createjs.com/docs/easeljs/classes/Stage.html)).

生成一个DisplayProps对象，该对象表示该对象及其所有父容器直到最高级祖先（通常是[stage](https://www.createjs.com/docs/easeljs/classes/Stage.html)）的组合显示属性。

Parameters:

    - [props]:A [DisplayProps](https://www.createjs.com/docs/easeljs/classes/DisplayProps.html) object to populate with the calculated values. If null, a new DisplayProps object is returned.:DisplayProps对象用计算填充的值。如果为null，则返回一个新的DisplayProps对象。

Returns:The combined display properties.(所有的展示属性)

- getConcatenatedMatrix

Generates a Matrix2D object representing the combined transform of the display object and all of its parent Containers up to the highest level ancestor (usually the Stage). This can be used to transform positions between coordinate spaces, such as with [localToGlobal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_localToGlobal) and [globalToLocal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_globalToLocal).

生成一个Matrix2D对象，该对象表示为显示对象及其所有父容器到最高级别祖先（通常是舞台）的组合变换。 这可以用于在坐标空间之间转换位置，例如[localToGlobal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_localToGlobal)和[globalToLocal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_globalToLocal)。

Parameters:
    
    - [matrix]:A [Matrix2D](https://www.createjs.com/docs/easeljs/classes/Matrix2D.html) object to populate with the calculated values. If null, a new Matrix2D object is returned.([Matrix2D](https://www.createjs.com/docs/easeljs/classes/Matrix2D.html)对象生成的计算后的值。如果为null，则返回一个新的Matrix2D对象)

Returns：
    The combined matrix.(生成的矩阵)

- getMatrix 
    
    Returns a matrix based on this object's current transform.

    基于该对象现在的变化返回一个矩阵

Parameters：
    
    matrix:A Matrix2D object to populate with the calculated values. If null, a new Matrix object is returned.(一个Matrix2D对象生成的计算后的值。如果为null，则返回一个新的Matrix2D对象)

Returns：

A matrix representing this display object's transform.(一个表示该展示对象变化的矩阵)

- getTransformedBounds ()

Returns a rectangle representing this object's bounds in its parent's coordinate system (ie. with transformations applied). Objects that have been cached will return the transformed bounds of the cache.

Not all display objects can calculate their own bounds (ex. Shape). For these objects, you can use setBounds so that they are included when calculating Container bounds.

To reduce memory impact, the returned Rectangle instance may be reused internally; clone the instance or copy its values if you need to retain it.

Container instances calculate aggregate bounds for all children that return bounds via getBounds.

返回表示此父母坐标系中此对象边界的矩形（即变换以后的矩形）。已缓存的对象将返回已缓存的转换后的边界。

并非所有显示对象都可以计算它们自己的边界（例如形状）。对于这些对象，可以使用setBounds，以便在计算容器边界时包含它们。

为了减少内存影响，返回的Rectangle实例可以在内部重用; 如果您需要保留它的话，您可以克隆实例或复制它的值。

Returns:

A Rectangle instance representing the bounds, or null if bounds are not available for this object.
一个代表边框的矩形，如果没有有效的对象，则返回null

- globalToLocal ( x, y, [pt])

Transforms the specified x and y position from the global (stage) coordinate space to the coordinate space of the display object. For example, this could be used to determine the current mouse position within the display object. Returns a Point instance with x and y properties correlating to the transformed position in the display object's coordinate space.

将指定的x和y位置从全局（stage）坐标空间转换为显示对象的坐标空间。例如，这可以用来确定显示对象内当前的鼠标位置。它会返回一个Point实例，其x和y属性与显示对象坐标空间中的变换后位置有关。

Example:

```
displayObject.x = 300;
displayObject.y = 200;
stage.addChild(displayObject);
var point = displayObject.globalToLocal(100, 100);
// Results in x=-200, y=-100
```

Parameters:

    - x:The x position on the stage to transform.(转变后x的位置)
    - y:The y position on the stage to transform.(转变后y的位置)
    - [pt] :An object to copy the result into. If omitted a new Point object with x/y properties will be returned.(一个复制结果的对象。如果省略，则返回一个具有x / y属性的新Point对象。)

Returns:
    
    A Point instance with x and y properties correlating to the transformed position in the display object's coordinate space.

    返回一个在展示对象上的坐标系上的x和y属性的点的实例

- hasEventListener 

    Indicates whether there is at least one listener for the specified event type.

    指明在是否至少有一种特定事件类型的监听器。

    Parameters:
        
        - type:The string type of the event.(字符串表示的事件类型)

    Returns:Returns true if there is at least one listener for the specified event.(如果至少有一种特定事件类型的监听器,则返回真)

- hitTest(x,y)

    Tests whether the display object intersects the specified point in local coordinates (ie. draws a pixel with alpha > 0 at the specified position). This ignores the alpha, shadow, hitArea, mask, and compositeOperation of the display object.

    测试显示对象是否与本地坐标中的指定点相交（即在指定位置绘制一个alpha> 0的像素）。它会忽略显示对象的alpha，shadow，hitArea，mask和compositeOperation。

Example:
    
```
stage.addEventListener("stagemousedown", handleMouseDown);
function handleMouseDown(event) {
    var hit = myShape.hitTest(event.stageX, event.stageY);
}
```

Please note that shape-to-shape collision is not currently supported by EaselJS.

注意：EaselJS目前不支持shape-to-shape碰撞。

Parameters:
    
    - x:The x position to check in the display object's local coordinates(检查显示对象的本地坐标的x位置)
    - y:The y position to check in the display object's local coordinates.(检查显示对象的本地坐标的y的位置)

Returns:
    
    A Boolean indicating whether a visible portion of the DisplayObject intersect the specified local Point.(返回一个布尔类型的值，指示DisplayObject的可见部分是否与指定的本地Point相交。)

- isVisible()

Returns true or false indicating whether the display object would be visible if drawn to a canvas. This does not account for whether it would be visible within the boundaries of the stage.

返回true或false，指示显示对象是否在绘制到画布时可见。这并没有能说明它是否在舞台边界内可见。

NOTE: This method is mainly for internal use, though it may be useful for advanced uses.

注意：这个方法主要用作内部使用，尽管它可以作为其他高级的使用。

Returns:

Boolean indicating whether the display object would be visible if drawn to a canvas

指明了如果画在canvas上要显示的对象是否可见。

- localToGlobal ( x, y,[pt])

Transforms the specified x and y position from the coordinate space of the display object to the global (stage) coordinate space. For example, this could be used to position an HTML label over a specific point on a nested display object. Returns a Point instance with x and y properties correlating to the transformed coordinates on the stage.


将指定的x和y位置从本地坐标系坐标空间转换为全局坐标空间。例如，这可以用来将HTML标签定位在嵌套显示对象上的特定位置上。它会返回一个Point实例，其x和y属性与显示对象坐标空间中的变换后位置有关。

Example:

```
displayObject.x = 300;
displayObject.y = 200;
stage.addChild(displayObject);
var point = displayObject.localToGlobal(100, 100);
// Results in x=400, y=300
```

Parameters:

    - x:The x position in the source display object to transform.(要显示的源显示对象中的x位置。)
    - y:The y position in the source display object to transform.(要显示的源显示对象中的y位置
。)
    - [pt] point|object:An object to copy the result into. If omitted a new Point object with x/y properties will be returned.(一个复制结果的对象。如果省略，则返回具有x / y属性的新Point对象。)

Returns:

     A Point instance with x and y properties correlating to the transformed coordinates on the stage.

     返回一个具有x和y属性，并与舞台上已转换的坐标相关联的点的实例。

- localToLocal 

Transforms the specified x and y position from the coordinate space of this display object to the coordinate space of the target display object. Returns a Point instance with x and y properties correlating to the transformed position in the target's coordinate space. Effectively the same as using the following code with [localToGlobal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_localToGlobal) and [globalToLocal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_globalToLocal).

将指定的x和y位置从此显示对象的坐标空间转换为目标显示对象的坐标空间。 返回一个Point实例，其中x和y属性与目标坐标空间中的变形位置相关。 与在[localToGlobal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_localToGlobal)和[globalToLocal](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_globalToLocal)中使用以下代码有效相同。

```
var pt = this.localToGlobal(x, y);
pt = target.globalToLocal(pt.x, pt.y);
```

Parameters:

    - x:The x position in the source display object to transform.(要显示的源显示对象中的x位置
。)
    - y:The y position on the source display object to transform.(要显示的源显示对象中的y位置。)
    - target:he target display object to which the coordinates will be transformed.(要转换为坐标系的源展示对象。)
    - [pt] Point | Object:An object to copy the result into. If omitted a new Point object with x/y properties will be returned.(一个复制结果的对象。如果省略，则返回具有x / y属性的新Point对象。)

Returns:

Returns a Point instance with x and y properties correlating to the transformed position in the target's coordinate space.

    返回一个Point实例，其中x和y属性与目标坐标空间中的变形位置相关。

off(type,listener,[useCapture])

A shortcut to the removeEventListener method, with the same parameters and return value. This is a companion to the .on method.

removeEventListener方法的快捷方式，具有相同的参数和返回值。常常与.on一起使用。

IMPORTANT: To remove a listener added with on, you must pass in the returned wrapper function as the listener. See [on](https://www.createjs.com/docs/easeljs/classes/EventDispatcher.html#method_on) for an example.

主要提示：为了删除添加了on的侦听器，您必须传入一个返回包装函数作为侦听器。 详情请参见[on](https://www.createjs.com/docs/easeljs/classes/EventDispatcher.html#method_on)的例子。

Parameters:

    - type:The string type of the event.(事件的字符串类型)
    - listener:The listener function or object.(监听函数或者对象)
    - [useCapture]:对于事件冒泡，指示是否在捕获或冒泡/目标阶段监听事件。

- on(type, listener, [scope], [once=false], [data], [useCapture=false])

A shortcut method for using addEventListener that makes it easier to specify an execution scope, have a listener only run once, associate arbitrary data with the listener, and remove the listener.

一种使用addEventListener的快捷方法，可以更轻松地指定执行范围，让侦听器只运行一次，将任意数据与侦听器关联，并删除侦听器。

This method works by creating an anonymous wrapper function and subscribing it with addEventListener. The wrapper function is returned for use with removeEventListener (or off).

此方法通过创建匿名包装函数并使用addEventListener对其进行描述。包装函数返回用于removeEventListener（或off）。

IMPORTANT: To remove a listener added with on, you must pass in the returned wrapper function as the listener, or use remove. Likewise, each time you call on a NEW wrapper function is subscribed, so multiple calls to on with the same params will create multiple listeners.

重要提示：要删除添加了on的侦听器，您必须将返回的包装器函数作为侦听器，或者使用remove。 同样，每次您调用NEW包装函数时，都会使用相同的参数进行多次调用，从而创建多个监听器。

Example：

```
var listener = myBtn.on("click", handleClick, null, false, {count:3});
    function handleClick(evt, data) {
        data.count -= 1;
        console.log(this == myBtn); // true - scope defaults to the dispatcher
        if (data.count == 0) {
            alert("clicked 3 times!");
            myBtn.off("click", listener);
            // alternately: evt.remove();
        }
    }
```
Parameters:

    - type: The string type of the event.(字符串类型的事件)
    - listener: An object with a handleEvent method, or a function that will be called when the event is dispatched.(带有handleEvent方法的对象，或在分派事件时将被调用的函数)
    - [scope] Object:The scope to execute the listener in. Defaults to the dispatcher/currentTarget for function listeners, and to the listener itself for object listeners (ie. using handleEvent).(指其中执行侦听器的作用域。缺省为函数侦听器的dispatcher / currentTarget，以及侦听器本身的对象侦听器（即使用handleEvent）。)
    - [once=false]:If true, the listener will remove itself after the first time it is triggered.(如果为真，则在第一次触发后移除事件)
    - [data]:Arbitrary data that will be included as the second parameter when the listener is called.(在调用监听器时将包含作为第二个参数的任意数据。)
    - [useCapture=false]:对于冒泡的事件，指示是否在捕获或冒泡/目标阶段监听事件。

Returns:
    
Returns the anonymous function that was created and assigned as the listener. This is needed to remove the listener later using .removeEventListener.

返回已创建并分配为侦听器的匿名函数。这需要删除稍后使用的.removeEventListener侦听器。

- removeAllEventListeners([type])

Removes all listeners for the specified type, or all listeners of all types.

移除所有特定类型的监听器，或者所有类型的监听器。

Example:
```
// Remove all listeners
displayObject.removeAllEventListeners();

// Remove all click listeners
displayObject.removeAllEventListeners("click");
```

Parameters:
    [type]:The string type of the event. If omitted, all listeners for all types will be removed.(事件的字符串类型。 如果省略，所有类型的所有侦听器都将被删除。)

removeEventListener( type, listener, [useCapture])

Removes the specified event listener.

移除特定事件的监听器。

Important Note: that you must pass the exact function reference used when the event was added. If a proxy function, or function closure is used as the callback, the proxy/closure reference must be used - a new proxy or closure will not work.

重要提示：您在添加事件时必须使用的特定的函数引用。如果使用代理函数或函数闭包作为回调函数，则必须使用代理/闭包引用 - 否则新代理或闭包将不起作用。

Example

```
displayObject.removeEventListener("click", handleClick);
```

Parameters:

    - type:The string type of the event.(字符串类型的事件)
    - listener:The listener function or object.(监听函数或者对象)
    - [useCapture]：For events that bubble, indicates whether to listen for the event in the capture or bubbling/target phase.(对于事件冒泡，指示是否在捕获或冒泡/目标阶段监听事件。)

- set(props)

Provides a chainable shortcut method for setting a number of properties on the instance.

可以为对象上一系列的属性提供链式的快捷方法。

Example:

```
var myGraphics = new createjs.Graphics().beginFill("#ff0000").drawCircle(0, 0, 25);
var shape = stage.addChild(new Shape()).set({graphics:myGraphics, x:100, y:100, alpha:0.5});
```
Parameters:

    - props:A generic object containing properties to copy to the DisplayObject instance.(包含要复制到DisplayObject实例的属性的通用对象。)

Returns:
    
    Returns the instance the method is called on (useful for chaining calls.)(返回调用该方法的实例（用于链接调用。）)

- setBounds ( x,y,width,height)

Allows you to manually specify the bounds of an object that either cannot calculate their own bounds (ex. Shape & Text) for future reference, or so the object can be included in Container bounds. Manually set bounds will always override calculated bounds.

允许您手动指定无法计算自己的边界（例如“形状和文本”）以供将来参考的对象边界，或者可以将对象包含在容器边界中。手动设置边界将始终覆盖计算边界。

The bounds should be specified in the object's local (untransformed) coordinates. For example, a Shape instance with a 25px radius circle centered at 0,0 would have bounds of (-25, -25, 50, 50).

边界应该在对象的本地（未转换的）坐标中指定。例如，具有以0,0为中心的25像素半径圆的Shape实例将具有（-25，-25，50，50）的范围。

Parameters:
    
    - x:The x origin of the bounds. Pass null to remove the manual bounds.(边界的x的原点。传递null会删除手动设置的边界。)
    - y:The y origin of the bounds.(边界的y的原点。)
    - width:The width of the bounds.(边界的宽度)
    - height:The height of the bounds.(边界的高度)

- setTransform( [x=0], [y=0], [scaleX=1], [scaleY=1], [rotation=0], [skewX=0], [skewY=0],[regX=0],[regY=0])

Shortcut method to quickly set the transform properties on the display object. All parameters are optional. Omitted parameters will have the default value set.

设置显示对象的变换属性的快速方法。所有参数都是可选的。省略参数将设置默认值。

Example:

```
displayObject.setTransform(100, 100, 2, 2);
```

Parameters:
    - [x=0]:The horizontal translation (x position) in pixels(水平平移（x位置），以像素为单位)
    - [y=0]:The vertical translation (y position) in pixels(垂直平移(y位置)，以像素为单位)
    - [scaleX=1]:The horizontal scale, as a percentage of 1(水平的量度，基本单位为百分之1)
    - [scaleX=1]:The vertical scale, as a percentage of 1(垂直的量度，基本单位为百分之1)
    - [rotation=0]:The rotation, in degrees(旋转的角度)
    - [skewX=0]:The horizontal skew factor(水平方向上的倾斜角度)
    - [skewY=0]:The vertical skew factor(垂直方向上的倾斜角度)
    - [regX=0]:The horizontal registration point in pixels(以像素为单位的水平标注点)
    - [regX=0]:The vertical registration point in pixels(以像素为单位的垂直标注点)
 
Returns:

    Returns this instance. Useful for chaining commands.(返回该实例，对于链式指令非常有用)

- toString ()
    
    Returns a string representation of this object.

    返回该对象的字符串表达式。

Returns:
    
    a string representation of the instance.(返回该对象的字符串表达式)

- uncache ()
    
   Clears the current cache. See [cache](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache) for more information.
   清除现在的缓存，请在[缓存](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_cache)查看更多信息


- updateCache ()

Redraws the display object to its cache. Calling updateCache without an active cache will throw an error. If compositeOperation is null the current cache will be cleared prior to drawing. Otherwise the display object will be drawn over the existing cache using the specified compositeOperation.

将显示对象设为缓存。在没有有效缓存的情况下调用updateCache会引发错误。如果compositeOperation为null，则在绘制之前将清除当前缓存。否则，该显示对象会将使用指定的compositeOperation绘制现有的缓存。

Example:

Clear the current graphics of a cached shape, draw some new instructions, and then update the cache. The new line will be drawn on top of the old one.

清除现有的缓存图像，绘制新的内容，然后更新缓存,同时新的一行将会绘制在老的缓存的上面。

```
 // Not shown: Creating the shape, and caching it.
 shapeInstance.clear();
 shapeInstance.setStrokeStyle(3).beginStroke("#ff0000").moveTo(100, 100).lineTo(200,200);
 shapeInstance.updateCache();
```

In previous versions caching was handled on DisplayObject but has since been moved to [BitmapCache](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html). This allows for easier interaction and alternate cache methods like WebGL and [StageGL](https://www.createjs.com/docs/easeljs/classes/StageGL.html).

在之前的版本中，缓存是在DisplayObject上处理的，但后来被移至[BitmapCache](https://www.createjs.com/docs/easeljs/classes/BitmapCache.html)。 这允许更简单的交互和替代缓存方法，如WebGL和[StageGL](https://www.createjs.com/docs/easeljs/classes/StageGL.html)。

Parameters:

The compositeOperation to use, or null to clear the cache and redraw it. [whatwg spec on compositing](https://html.spec.whatwg.org/multipage/scripting.html#dom-context-2d-globalcompositeoperation).

要使用的compositeOperation，如果设为null，则清除缓存并重新绘制它。[whatwg spec on compositing](https://html.spec.whatwg.org/multipage/scripting.html#dom-context-2d-globalcompositeoperation).

- updateContext(ctx)

Applies this display object's transformation, alpha, globalCompositeOperation, clipping path (mask), and shadow to the specified context. This is typically called prior to [draw](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_draw).

将此展示对象的变换，alpha，globalCompositeOperation，剪切路径（蒙层）和阴影应用于指定的内容上。这通常在[绘制](https://www.createjs.com/docs/easeljs/classes/DisplayObject.html#method_draw)之前调用。

- willTrigger(type)

Indicates whether there is at least one listener for the specified event type on this object or any of its ancestors (parent, parent's parent, etc). A return value of true indicates that if a bubbling event of the specified type is dispatched from this object, it will trigger at least one listener.

指示此对象或其任何祖先（父，父母的父级等）上的指定事件类型是否至少有一个侦听器。返回值为true表示如果从此对象分派指定类型的冒泡事件，它将触发至少一个侦听器。

This is similar to [hasEventListener](https://www.createjs.com/docs/easeljs/classes/EventDispatcher.html#method_hasEventListener), but it searches the entire event flow for a listener, not just this object.

这与[hasEventListener](https://www.createjs.com/docs/easeljs/classes/EventDispatcher.html#method_hasEventListener)类似，但是它只会搜索监听器的事件流，而不是整个对象。

Parameters:
    
    - type(事件的字符串类型。)

Returns:
    
    Returns true if there is at least one listener for the specified event.

    如果有至少一个特定事件的监听器，则返回true
