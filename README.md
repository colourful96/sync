# 2023

### 11-24

1. 使用node的http模块启动一个服务（不使用express），使用cors解决跨域

   ```
   const server = http.createServer((req, res) => {
       handleReq(req);
       res.setHeader('Access-Control-Allow-Origin', 'xxx')
       res.setHeader('Access-Control-Allow-Credentials', true)
   
       res.statusCode = 200;
       res.write("你好！");
       res.end();
   });
   ```

2. 常见的地图服务（WMS/WFS/WCS/TMS/WMTS）

3. 3D Tiles简介 [简介](https://gitee.com/link?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F389652357)

### 11-27

1. fiber节点，fiberTree的深度优先遍历

### 11-28

1. POI是Point of Interest的缩写，是指兴趣点。每个POI至少包含以下4项基本信息：名称（Name）、类别（Type）、经度（longitude）、纬度（latitude），所以poiName指的是兴趣点名称，它可以是一栋房子、一个商铺、一个公厕或一个公交站等。
2. AOI是Area of interest的缩写，代指兴趣面。AOI同样包含4项基本信息：名称（Name）、类别（Type）、经度（longitude）、纬度（latitude），指的是地图数据中的区域状的地理实体。

### 11-29

1. border:dotted，边框设置虚线后无法修改点与点之间的距离，可通过背景色的方式实现

   ```javascript
   // 横
   .hor{
         height: 1px;
         background-image: linear-gradient(to right, #E7C737 0%, #28B35B 50%, transparent 0%);
         background-size: 14px 1px;
         background-repeat: repeat-x;
       }
   // 竖
    .vec{
        width: 1px;
         background-image: linear-gradient(to bottom, #E7C737 0%, #28B35B 50%, transparent 0%);
         background-size: 1px 14px;
         background-repeat: repeat-y;
       }
   // 调整background-size可调整距离
   ```

### 12-04

1. 使用express获取不到post请求的参数，可能需要中间件来解析请求参数

   ```javascript
   app.use(express.json()); // 解析 JSON 请求体
   app.use(express.urlencoded({ extended: true })); // 解析 URL 编码的请求体
   
   app.post('/search', function(req, res) {
     console.log(req.body); // 确认请求体参数是否被正确解析
     const { areaName } = req.body;
     // 处理参数
     // ...
   });
   ```

### 12-05

1. 函数组件中`React.memo`第二个参数可实现和类组件中`shouldComponentUpdate`生命周期方法同样的功能。

   ```javascript
   import React, { memo } from 'react';
   
   function MyComponent(props) {
     // ...
   }
   
   function areEqual(prevProps, nextProps) {
     // 自定义比较逻辑，判断 props 是否相等
     return prevProps.name === nextProps.name;
   }
   
   export default memo(MyComponent, areEqual);
   ```

2. `navigator.getBattery()`可获取电脑的充电信息，当电量和充电状态发生变化会触发相应的事件

   ```javascript
   navigator.getBattery().then(function(battery) {
     console.log('当前电量：', battery.level * 100 + '%');
     console.log('是否正在充电：', battery.charging ? '是' : '否');
   
     // 添加事件监听器
     battery.addEventListener('chargingchange', function() {
       console.log('充电状态发生变化');
       console.log('当前充电状态：', battery.charging ? '充电中' : '未充电');
     });
   
     battery.addEventListener('levelchange', function() {
       console.log('电量发生变化');
       console.log('当前电量：', battery.level * 100 + '%');
     });
   });
   ```

### 12-11

1. echarts中折线图自定义拐点样式

### 12-13

1. svg中`path`绘制弧线，设置第三个参数旋转角度不生效

2. 网页中嵌入其他内容`<iframe>`,`<object>`,`<embed>`

   [参考](https://gitee.com/link?target=https%3A%2F%2Fjuejin.cn%2Fs%2Fhtml%20iframe%20object%20embed)

3. 伪类和伪元素

   > 伪类：
   >
   > - `:hover`：选择鼠标悬停在元素上的状态。
   > - `:active`：选择元素被激活或点击时的状态。
   > - `:focus`：选择元素获得焦点时的状态。
   > - `:first-child`：选择元素作为其父元素的第一个子元素。
   > - `:last-child`：选择元素作为其父元素的最后一个子元素。
   > - `:nth-child(n)`：选择元素作为其父元素的第 n 个子元素。
   >
   > 伪元素：
   >
   > - `::before`：在元素的内容前面添加样式。
   > - `::after`：在元素的内容后面添加样式。
   > - `::first-letter`：选择元素的第一个字母。
   > - `::first-line`：选择元素的第一行。
   > - `::selection`：选择元素的文本选中状态。
   >
   > 伪类和伪元素的区别在于它们选择元素的方式不同。伪类是针对元素的状态或属性进行选择，而伪元素是选择元素的内容。
   >
   > 伪类和伪元素的语法不同。伪类使用单冒号（:），而伪元素使用双冒号（::）。同时，伪元素只能用于某些元素，例如 `<p>`、`<h1>`、`<div>` 等，而不能用于表单元素。

### 12-15

1. 页面中引入canvas元素，当鼠标点击canvas元素时，获取到鼠标点击的位置转换成WebGL坐标

   ```javascript
   const canvas = document.getElementById('canvas');
   const rect = canvas.getBoundingClientRect();
   const x = event.clientX;
   const y = event.clientY;
    x = ((x - rect.left) - canvas.width/2)/(canvas.width/2);
    y = (canvas.height/2 - (y - rect.top))/(canvas.height/2);
   ```

### 12-18

**在WebGL中创建着色器（shader）的流程**

1. 创建着色器对象： 使用 WebGL 上下文的 `createShader` 方法创建一个着色器对象。着色器对象有两种类型：顶点着色器（`gl.VERTEX_SHADER`）和片元着色器（`gl.FRAGMENT_SHADER`）。
2. 编译着色器源代码： 使用 `shaderSource` 方法将着色器源代码分配给着色器对象。源代码是一个包含 GLSL（OpenGL Shading Language）代码的字符串。
3. 编译着色器： 使用 `compileShader` 方法编译着色器对象。这将把源代码编译成可供 GPU 使用的二进制代码。
4. 检查编译错误： 使用 `getShaderParameter` 方法和 `getShaderInfoLog` 方法检查编译是否成功，并获取编译过程中的错误信息（如果有）。
5. 创建着色器程序对象： 使用 `createProgram` 方法创建一个着色器程序对象。着色器程序是由一个顶点着色器和一个片元着色器组成的。
6. 附加着色器对象到着色器程序对象： 使用 `attachShader` 方法将顶点着色器和片元着色器附加到着色器程序对象上。
7. 链接着色器程序： 使用 `linkProgram` 方法链接着色器程序对象。这将把顶点着色器和片元着色器连接到一个可供使用的着色器程序中。
8. 检查链接错误： 使用 `getProgramParameter` 方法和 `getProgramInfoLog` 方法检查链接是否成功，并获取链接过程中的错误信息（如果有）。
9. 使用着色器程序： 使用 `useProgram` 方法将着色器程序设置为当前的渲染状态，以便在绘制过程中使用该着色器程序。

### 12-19

1. Ant Design Vue使用Table组件需要设置key。

   ```javascript
   // 在数据中设置key值
   data() {
     return {
       dataSource: [
         { key: '1', name: 'John Doe', age: 25 },
         { key: '2', name: 'Jane Smith', age: 30 },
         // ...
       ],
     };
   },
   // 设置rowKey属性
   <a-table :data-source="dataSource" rowKey="id">
     <!-- 表格列配置 -->
   </a-table>  
   ```

2. Ant Design Vue使用带有插槽的组件时，会提示`slot`和`slot-scope`已经过期。以下时替代写法，`Table`组件为例

   ```javascript
   // 已过时
   <template v-slot='operation' slot-scope='text, record'>
   </template>
   
   <template #operation="text, record" >
   </template>
   const columns = [
    {
             title: '操作',
             dataIndex: 'operation',
             scopedSlots: {customRender: 'operation'},
           },
   ]
   ```

3. 在 WebGL 中，`gl.bindBuffer(target, buffer)` 函数用于将一个缓冲区对象绑定到目标上。其中，`target` 参数表示目标类型，可以是 `gl.ARRAY_BUFFER`、`gl.ELEMENT_ARRAY_BUFFER` 等，而 `buffer` 参数表示要绑定的缓冲区对象。

   在函数 `gl.bindBuffer(gl.ARRAY_BUFFER, vertexColorBuffer)` 中，我们将缓冲区对象 `vertexColorBuffer` 绑定到目标 `gl.ARRAY_BUFFER` 上，以便存储顶点属性数据。而在 `gl.bindBuffer(gl.ARRAY_BUFFER, null)` 中，我们将目标 `gl.ARRAY_BUFFER` 解除绑定，以确保不会意外地修改该目标的状态。

   在 WebGL 中，每个目标只能绑定一个缓冲区对象。如果我们在设置顶点属性指针之前没有解除 `gl.ARRAY_BUFFER` 目标的绑定，则可能会意外地修改该目标的状态，从而导致错误。因此，在设置完顶点属性指针之后，我们需要将 `gl.ARRAY_BUFFER` 目标解除绑定，以确保不会意外地修改该目标的状态。

### 12-20

1. 谷歌浏览器设置允许访问本地文件的方式。
2. 可浏览器中的接口请求复制（copy as cURL）,在apifox中导入，可以将整个接口请求（header,cookie）等信息全部复制。

### 12-21

1. WebGL课程纹理。

### 12-25

1. vue当中事件修饰符。

2. 正射投影与透视投影的区别。

   > 正射投影是一种平行投影方式，它将场景中的物体投影到一个平面上，并保持物体在投影中的大小不变。在正交投影中，场景中的物体在屏幕上呈现相同大小，无论它们在场景中的距离如何。因此，正交投影通常用于 2D 游戏或 UI 界面等场景。
   >
   > 透视投影是一种透视投影方式，它将场景中的物体投影到一个透视平面上，并根据物体在场景中的距离缩放物体的大小。在透视投影中，场景中的物体在屏幕上呈现不同大小，距离相机越远的物体在屏幕上呈现越小。因此，透视投影通常用于 3D 场景中，以创建更加真实的视觉效果。
   >
   > 在 WebGL 中，正射投影和透视投影可以通过设置投影矩阵来实现。正射投影矩阵可以使用 `setOrtho()` 方法来创建，透视投影矩阵可以使用 `setPerspective()` 方法来创建。在实际应用中，你可以根据场景的需要选择使用哪种投影方式。

### 12-26

1. 浏览器控制台中，如果一个 JavaScript 对象的字段是灰色的，这意味着该字段是对象的一个属性，但是它当前不可枚举，也就是说它不会出现在对象的 `for...in` 循环中，也不会被 `Object.keys()` 等方法返回。可以使用 `Object.getOwnPropertyNames()` 方法查看对象的所有属性。

### 12-28

1. 类型化数组

   > 1. Int8Array、Uint8Array、Uint8ClampedArray：用于处理8位整数（有符号、无符号、固定范围）。
   > 2. Int16Array、Uint16Array：用于处理16位整数（有符号、无符号）。
   > 3. Int32Array、Uint32Array：用于处理32位整数（有符号、无符号）。
   > 4. Float32Array：用于处理32位浮点数。
   > 5. Float64Array：用于处理64位浮点数。

### 12-29

1. 物体表面的朝向（法线）

   > 物体表面的朝向是指表面在每个点处的法线方向。法线是垂直于表面的矢量，指示了表面的朝向和方向。在计算机图形学中，法线在渲染和光照计算中起着重要的作用。
   >
   > 对于平面几何体（如矩形或三角形），法线是固定的，与平面的朝向相对应。例如，一个水平的矩形表面的法线指向上方，而一个垂直于地面的矩形表面的法线指向前方。
   >
   > 对于复杂的曲面或三维模型，法线的计算通常是通过对表面的顶点进行插值得到的。在这种情况下，通常使用三角形来近似曲面。每个三角形的法线由其三个顶点的法线插值得到。这种插值法线的计算可以使用向量运算和数学方法来实现。
   >
   > 法线在渲染中的重要性在于它们与光照计算密切相关。光照模型通常使用表面法线来计算光线与表面的相互作用。例如，根据光线的方向和表面法线的方向，可以计算出光线的入射角度和表面的漫反射强度。这对于产生逼真的光照效果非常重要。
   >
   > 在计算机图形学中，法线还可以用于其他操作，例如投影、纹理映射、碰撞检测等。在处理复杂的三维模型时，准确计算和使用正确的法线是实现真实感渲染和模拟物理行为的关键。

2. 点积运算，归一化运算，GLSL ES语言已经内置。

3. webgl中光线的方式为什么使用世界坐标系？世界坐标系与局部坐标系。

4. gl.uniform3f 和 gl.uniform3fv用法

5. 计算顶点的世界坐标：顶点坐标*模型矩阵

# 2024

### 1-2

1. github在验证git操作时已经不再接受账户密码。在sourceTree推送会失败。

   在github创建个人访问令牌（经典模式）

   在sourceTree中打开仓库设置，将远程URL修改为：

   ```javascript
   https://<令牌>@github.com/xxxx/sync.git
   ```

2. gl.unform3f和gl.unifrom3fv都是WebGL中用于设置3维向量类型的uniform变量的函数，区别在于他们接受参数方式不同

   ```javascript
   const location = gl.getUniformLocation(program, 'uColor');
   gl.uniform3f(location, 1.0, 0.0, 0.0);
   
   const location = gl.getUniformLocation(program, 'uColor');
   const value = [1.0, 0.0, 0.0];
   gl.uniform3fv(location, value);
   
   ```

3. WebGL中常见的坐标系以及区别？