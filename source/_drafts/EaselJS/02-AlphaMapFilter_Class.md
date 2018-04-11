# AlphaMapFilter Class(AlphaMapFilter 类)

------

Extends: [Filter](https://www.createjs.com/docs/easeljs/classes/Filter.html)

Defined in: [AlphaMapFilter:41](https://www.createjs.com/docs/easeljs/files/easeljs_filters_AlphaMapFilter.js.html#l41)

Module: [EaselJS](https://www.createjs.com/docs/easeljs/modules/EaselJS.html)

扩展于: [Filter](https://www.createjs.com/docs/easeljs/classes/Filter.html)

定义于: [AlphaMapFilter:41](https://www.createjs.com/docs/easeljs/files/easeljs_filters_AlphaMapFilter.js.html#l41)

模块: [EaselJS](https://www.createjs.com/docs/easeljs/modules/EaselJS.html)

Applies a greyscale alpha map image (or canvas) to the target, such that the alpha channel of the result will be copied from the red channel of the map, and the RGB channels will be copied from the target.

将灰度alpha图层的图像(或canvas)应用于对应目标上，这样可以将图像的红色通道复制到alpha通道，并且会从目标处复制RGB通道。

Generally, it is recommended that you use [AlphaMaskFilter](https://www.createjs.com/docs/easeljs/classes/AlphaMaskFilter.html), because it has much better performance.

通常，建议您使用[AlphaMaskFilter](https://www.createjs.com/docs/easeljs/classes/AlphaMaskFilter.html)，因为它有更好的表现。

Example（示例）

This example draws a red->blue box, caches it, and then uses the cache canvas as an alpha map on a 100x100 image.

这个例子会画一个颜色从红到蓝的盒子并缓存它，然后在一个100x100的图像上用缓存的canvas作为alpha图层。

```
 var box = new createjs.Shape();
 box.graphics.beginLinearGradientFill(["#ff0000", "#0000ff"], [0, 1], 0, 0, 0, 100)
 box.graphics.drawRect(0, 0, 100, 100);
 box.cache(0, 0, 100, 100);

 var bmp = new createjs.Bitmap("path/to/image.jpg");
 bmp.filters = [
    new createjs.AlphaMapFilter(box.cacheCanvas)
 ];
 bmp.cache(0, 0, 100, 100);
 stage.addChild(bmp);
```

## Constructor(构造函数)

AlphaMapFilter ( alphaMap )

Parameters(参数)：

- alphaMap HTMLImageElement | HTMLCanvasElement

The greyscale image (or canvas) to use as the alpha value for the result. This should be exactly the same dimensions as the target.

将灰度图像（或画布）作为结果的Alpha值。注意这个图像应该与目标尺寸完全相同。

### Methods:

- \_applyFilter ( imageData ) (belongs to Boolean)
    Parameters:
        imageData ImageData
        Target ImageData instance.
    Returns:
        Boolean.

- applyFilter ( ctx, x, y,  width,  height,  [targetCtx],  [targetX],  [targetY] ) (belongs to Boolean)
    
    Applies the filter to the specified context.

    将filter应用与特定的内容上。
    
    Parameters:
      
      1. ctx CanvasRenderingContext2D:The 2D context to use as the source.（作为源文件的2D的内容）
      
      2. x:The x position to use for the source rect.(用于源矩形上x坐标的位置)
    
      3. y:The y position to use for the source rect.(用于源矩形上y坐标的位置)

      4. width:The width to use for the source rect.(源矩形的宽度)

      5. height:The height to use for the source rect.(源矩形的高度)

      6. [targetCtx] CanvasRenderingContext2D (optional可选):The 2D context to draw the result to. Defaults to the context passed to ctx.(绘制到结果上的2D内容。默认为ctx)

      7. [targetX]（optional 可选): The x position to draw the result to. Defaults to the value passed to x.（绘制到结果上的2D内容。默认为x的值）

      8. [targetY]（optional 可选): The y position to draw the result to. Defaults to the value passed to y.（绘制>到结果上的2D内容。默认为y的值）

    Returns:

      Boolean: If the filter was applied successfully.(返回true/false)

- clone ()
    
     Returns a clone of this Filter instance.

     返回克隆的Filter的实例

- getBounds( [rect] )

     Provides padding values for this filter. That is, how much the filter will extend the visual bounds of an object it is applied to.

     为此过滤器提供内边距值。也就是说，过滤器将这个值扩展到对象的可视范围。

     Parameters: [rect](optional)

     If specified, the provided Rectangle instance will be expanded by the padding amounts and returned.

     如果指定，则提供的Rectangle实例将被内边距的值扩展并返回。

     Returns:

     If a rect param was provided, it is returned. If not, either a new rectangle with the padding values, or null if no padding is required for this filter.

     如果提供了矩形参数，则返回该参数。否则，则返回带有内边距的新矩形，如果对于此过滤器没有要求，则返回null

- shaderParamSetup ( gl, stage, shaderProgram )
    
     Assign any unique uniforms or other setup functionality here.

     此方法会分配任何独特的属性或其他设置功能。

     Parameters:

        1. gl WebGLContext:The context associated with the stage performing the render.(与stage的渲染表现相关)

        2. stage:The stage instance that will be rendering.(要被渲染的stage实例)

        3. shaderProgram: The compiled shader that is going to be used to perform the render.(用于渲染的编译后的着色器)

- toString ()
    
        Returns a string representation of this object.

        返回该对象的字符串表达式。

### Properties

- alphaMap HTMLImageElement | HTMLCanvasElement

    The greyscale image (or canvas) to use as the alpha value for the result. This should be exactly the same dimensions as the target.

    将灰度图像（或画布）作为结果的Alpha值。注意这个图像应该与目标尺寸完全相同。
    
- FRAG_SHADER
    
    Pre-processed template shader code. It will be parsed before being fed in into the shader compiler. This should be based upon StageGL.SHADER_FRAGMENT_BODY_REGULAR

    预处理的模板着色器代码。在开始被着色器编译器前应当先被解析。这应该基于StageGL.SHADER_FRAGMENT_BODY_REGULAR

- usesContext 

    A flag stating that this filter uses a context draw mode and cannot be batched into imageData processing. Default: false
    
    一个使用此过滤器进行上下文绘制模式的标志，不能批量处理imageData。默认为false

- VTX_SHADER

    Pre-processed template shader code. It will be parsed before being fed in into the shader compiler. This should be based upon StageGL.SHADER_VERTEX_BODY_REGULAR

    预处理的模板着色器代码。在开始被着色器编译器前应当先被解析。这应该基于StageGL.SHADER_VERTEX_BODY_REGULAR
