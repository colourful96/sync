# 2023

### 11-24

1. 使用 node 的 http 模块启动一个服务（不使用 express），使用 cors 解决跨域

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

3. 3D Tiles 简介 [简介](https://gitee.com/link?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F389652357)

### 11-27

1. fiber 节点，fiberTree 的深度优先遍历

### 11-28

1. POI 是 Point of Interest 的缩写，是指兴趣点。每个 POI 至少包含以下 4 项基本信息：名称（Name）、类别（Type）、经度（longitude）、纬度（latitude），所以 poiName 指的是兴趣点名称，它可以是一栋房子、一个商铺、一个公厕或一个公交站等。
2. AOI 是 Area of interest 的缩写，代指兴趣面。AOI 同样包含 4 项基本信息：名称（Name）、类别（Type）、经度（longitude）、纬度（latitude），指的是地图数据中的区域状的地理实体。

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

1. 使用 express 获取不到 post 请求的参数，可能需要中间件来解析请求参数

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

1. echarts 中折线图自定义拐点样式

### 12-13

1. svg 中`path`绘制弧线，设置第三个参数旋转角度不生效

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

1. 页面中引入 canvas 元素，当鼠标点击 canvas 元素时，获取到鼠标点击的位置转换成 WebGL 坐标

   ```javascript
   const canvas = document.getElementById('canvas');
   const rect = canvas.getBoundingClientRect();
   const x = event.clientX;
   const y = event.clientY;
    x = ((x - rect.left) - canvas.width/2)/(canvas.width/2);
    y = (canvas.height/2 - (y - rect.top))/(canvas.height/2);
   ```

### 12-18

**在 WebGL 中创建着色器（shader）的流程**

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

1. Ant Design Vue 使用 Table 组件需要设置 key。

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

2. Ant Design Vue 使用带有插槽的组件时，会提示`slot`和`slot-scope`已经过期。以下时替代写法，`Table`组件为例

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
2. 可浏览器中的接口请求复制（copy as cURL）,在 apifox 中导入，可以将整个接口请求（header,cookie）等信息全部复制。

### 12-21

1. WebGL 课程纹理。

### 12-25

1. vue 当中事件修饰符。

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

   > 1. Int8Array、Uint8Array、Uint8ClampedArray：用于处理 8 位整数（有符号、无符号、固定范围）。
   > 2. Int16Array、Uint16Array：用于处理 16 位整数（有符号、无符号）。
   > 3. Int32Array、Uint32Array：用于处理 32 位整数（有符号、无符号）。
   > 4. Float32Array：用于处理 32 位浮点数。
   > 5. Float64Array：用于处理 64 位浮点数。

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

2. 点积运算，归一化运算，GLSL ES 语言已经内置。

3. webgl 中光线的方式为什么使用世界坐标系？世界坐标系与局部坐标系。

4. gl.uniform3f 和 gl.uniform3fv 用法

5. 计算顶点的世界坐标：顶点坐标\*模型矩阵

# 2024

## 一月

### 1-2

1. github 在验证 git 操作时已经不再接受账户密码。在 sourceTree 推送会失败。

   在 github 创建个人访问令牌（经典模式）

   在 sourceTree 中打开仓库设置，将远程 URL 修改为：

   ```javascript
   https://<令牌>@github.com/xxxx/sync.git
   ```

2. gl.unform3f 和 gl.unifrom3fv 都是 WebGL 中用于设置 3 维向量类型的 uniform 变量的函数，区别在于他们接受参数方式不同

   ```javascript
   const location = gl.getUniformLocation(program, 'uColor');
   gl.uniform3f(location, 1.0, 0.0, 0.0);

   const location = gl.getUniformLocation(program, 'uColor');
   const value = [1.0, 0.0, 0.0];
   gl.uniform3fv(location, value);

   ```

3. WebGL 中常见的坐标系以及区别？

### 1-3

1. 前端中的路由不区分大小写，需要根据路由路径做判断时，最好全部转换大小写。

### 1-4

1. 一台电脑上可能会同时使用多个不同平台的仓库（github, gitee, 企业内部等）。在 git 配置时，为每个项目单独设置用户名和邮箱。不使用全局配置。
2. 漫游式引导，用户第一次访问时会有一个引导提示功能。
3. `precision mediump float;`语句用于指定浮点数的精度。它告诉着色器使用中等精度的浮点数来表示和计算浮点数值。以在保持较好图像质量的同时，减少对 GPU 资源的需求。语句只适用于片元着色器中的浮点数类型（如`float`、`vec2`、`vec3`等）。对于其他类型（如整数类型、布尔类型等），并不受该语句的影响。

### 1-5

1. WebGL 调试工具。[Spector.js](https://github.com/BabylonJS/Spector.js)
2. WebGL 中立方体的每个面加载纹理图片。
3. vuex 的经典案例，用户登录，鉴权，导航守卫。

### 1-7

1. webpack-bundle-analyzer 代码包大小分析工具。可根据不同的环境决定是否开启，一般只在生产环境开启。
2. 网站图标使用 shortcut icon。
3. Vue 中异步组件。
4. 使用 Vue/cli 脚手架创建的项目可以在浏览器使用`proecss`，是因为脚手架注入的一些代码，方便在浏览器区分环境。

### 1-8

1. 投影矩阵：定义可视空间，观察者的可视深度。

2. 视图矩阵：观察者的位置。

3. 模型矩阵：物体的变换（平移，缩放，旋转）。

4. 模型视图投影矩阵：三者的乘积，在 js 中计算完传给顶点着色器。

   1. 旋转动画：`requestAnimationFrame()` 只是请求浏览器在适当的时机调用参数函数，所以调用函数的间隔不固定，那么每次调用时简单的加上一个固定的角度值就会导致不可控制加速或减速效果。所以需要根据前后调用时间来确定旋转角度。

```javascript
 let g_last = Date.now();

    function animate(angle) {
        const now = Date.now();
        const elapsed = now - g_last;
        g_last = now;
        let newAngle = angle + (angle_step * elapsed) / 1000.0;
        return newAngle %= 360;
    }
```

### 1-9

1. 绘制出立方体，给立方体每个表面设置编号，点击立方体表面获取编号时有时获取到错误编号。
2. 隐藏面消除的原理。
3. 颜色缓冲区：用于存储渲染结果的一块内存区域。它保存了每个像素的颜色值，以便在渲染完成后将图像显示在屏幕上。
4. 整理 three.js 的学习资料。

### 1-10

1. 材质的分类。镜面高光与漫反射高光。

### 1-11

1. 一台电脑需要可能需要多个不同平台的远程仓库，而且有不同的邮箱地址。如果已经设置了全局的用户名和邮箱，可通过命令删除。

   ```javascript
   git config  --global --unset user.name git config --global --unset user.email
   // 对于非全局配置，去掉global即可
   ```

2. BufferGeometry 已经替代原有的 Geometry。使用 `THREE.Face3` 对象，你可以定义一个三角形面，并将其添加到 `Geometry` 对象中。然而，自 Three.js r125 版本开始，推荐使用 `BufferGeometry` 和 `BufferAttribute` 来代替 `THREE.Face3`，因为它们提供了更高效和灵活的方式来处理几何体数据。

### 1-12

1. 通过 npm 下载 threejs 的完整包（包含示例和附加组件）。如果需要用到附加组件需要单独引入。

### 1-15

1. 在计算机图形学和 Three.js 中，Lambert 材质是一种基础的光照模型，它模拟了漫反射（Diffuse Reflection）现象。漫反射是指光线照射到物体表面时，光线会以各种方向均匀散射的现象，其亮度与光源入射角无关。

2. `THREE.MeshLambertMaterial`材质在 r160 版本中设置自发光生效，设置点光源并没有效果，需要使用 r151 版本。

   在 Three.js 中，`THREE.MeshLambertMaterial` 类代表了 Lambert 材质，它的特点是：

   1. **漫反射光照**：Lambert 材质只考虑环境光和光源的漫反射部分，不考虑镜面高光效果。
   2. **颜色计算**：根据光源的颜色、强度以及表面法线与光源方向的角度来计算物体表面的颜色。当表面法线与光源方向越接近平行时，表面接收的光照越强；反之则越弱。
   3. **自发光**：可以设置一个自发光颜色，即使没有外部光源，对象也会发出一定的亮度。

3. 纹理和灰度纹理的区别？

4. 正交投影照相机`(right - left)`与`(top - bottom)`的比值跟`canvas`宽高比例一致。

### 1-16

1. ant-design-vue，vue-router 嵌套路由，当切换路由时`a-menu`组件是需要更换默认选中值，才能有选中状态的更改。

2. ```javascript
   let a = [];
   const b = [1,2,{a:'a'}];
   [,,a] = b;
   ```

3. Vue 插件定义

   ```javascript
   export default {
     install(Vue) {
       Vue.prototype.$start = function(){ ... };
     }
   };

   // main.js
   import Vue from 'vue';
   import MyPlugin from './plugin.js';
   Vue.use(MyPlugin);
   ```

4. `Phone`材质，`MeshPhongMaterial`在 r160 本本中设置点光源看不到物体，设置环境光没有镜面高光效果。需要使用 r151 版本。
5. `Lambert`和`Phong`材质在 r160 版本中的使用没有效果解决？

### 1-17

1. 在 WebGL 和原生 js 中使用`requestAnimationFrame`实现旋转动画，每次增加固定的角度值，在 WebGL 中转速越来越快，而在原生 js 中却是匀速旋转。
2. notion 中新建一个记录包的页面。
3. 法线材质调试场景使用。
4. [纹理贴图](https://threejs.org/docs/index.html?q=tex#api/zh/textures/Texture)的各个属性。

### 1-22

1. A instances B A 的原型链上是否有 B 的原型。

### 1-23

1. vuex 中怎么实现类似于`yield all()`的效果，同时发送多个请求。
2. 材质的 ambient 属性定义了材质对环境光照的响应颜色。当一个场景中有环境光时，环境光会均匀地影响场景中的所有物体，而物体材质的 ambient 属性决定了它如何吸收和反映这种环境光照。如果你设置了材质的 ambient 属性并且场景中存在环境光，那么物体的实际颜色将是材质的 ambient 属性值与环境光颜色的乘积。
3. 渲染流水线

### 1-24

1. ThreeJS 中的 UV 映射。UV 映射是一种将纹理坐标映射到几何体表面的过程。UV 坐标是二维坐标系，用于确定纹理在几何体表面上的位置。UV 映射允许将纹理图像贴附到几何体上，使其具有细节、颜色和纹理。
2. 着色器可以写在单独的文件中，也可以写在`script`标签中。
3. `THREE.AxisHelper()` 方法用于创建一个辅助对象，用于可视化坐标轴。
4. data.gui 创建简单的界面组件。

### 1-26

1. 对称加密于非对称加密区别，使用场景。
2. 使用`MessageChannel`和`iframe`进行通信。
3. 在 notion 上整理面试题。

### 1-29

1. three.js 中的粒子系统，创建粒子流程。
2. `Math.random()*10-5`。
3. vue/cli 脚手架提供了现代模式的命令来支持最新浏览器的生成环境的构建。`index.html`中可以使用[lodash template]([lodash template](https://lodash.com/docs/4.17.10#template))语法插入内容。
4. 无界面（无头）浏览器。node 实现 pdf 下载。

### 1-31

1. echarts 中的`graphic`原生图形元素组件。
2. 配置了`graphic`后使用 html2canvas 截图时，设置允许跨域，还是报错画布被污染，无法转换为图片。需要配置图片为`base64`格式。
3. 颜色空间。RGB(红绿蓝)、CMYK(青品黄黑)、HSL(色相饱和度亮度)

## 二月

### 2-2

1. 球坐标系。

### 2-5

1. ```html
   <div id='box'>
     <span>
       <span>
       	<input />
       </span>
     </span>
   </div>
   <script>
   	const box = document.getElementById('box');
     const input = box.querySelector('input');
   </script>
   ```

2. 透视投影相机设置视锥体比例`(window.innerWidth / window.innerHeight) * 0.5`，相机的视锥体宽度变为高度的一半。这意味着相机会将场景中的物体在水平方向上进行更少的投影。此时看到的物体在水平方向上会变长。

### 2-19

1. `touch-action`用于设置触摸屏用户如何操纵元素的区域。

2. `pointermove`使用指针设备（如鼠标、触摸屏或触控笔）移动指针时触发的事件。

3. `event.isPrimary` 是指针事件对象（如 `pointerdown`、`pointermove`、`pointerup` 等）的一个属性，用于判断事件是否为主要指针事件。

4. [Vue 中的插件](https://v2.cn.vuejs.org/v2/guide/plugins.html)，为 Vue 添加全局功能。

5. 相机绕场景中心旋转

   ```javascript
   let theta = 0, radius = 5;
   render(){
         theta += 0.1;
         // 相机绕场景中心旋转
         camera.position.x = radius * Math.sin( THREE.MathUtils.degToRad( theta ) );
         camera.position.y = radius * Math.sin( THREE.MathUtils.degToRad( theta ) );
         camera.position.z = radius * Math.cos( THREE.MathUtils.degToRad( theta ) );
         camera.lookAt(scene.position);

         renderer.render(scene,camera);

     	requestAnimationFrame(render);
   }
   ```

6. 通过光线投射（Raycaster）可判断鼠标指针是否移过了物体。

### 2-20

1. 可对 Vue 组件进行封装，添加多个混合，处理公共逻辑。
2. `JSON.parse('111')`是可以转换的。

### 2-22

1. 低代码平台中组件复制怎么实现？每个组件都时 json 数据，数据中定义了组件的样式、属性、事件等信息，复制 json 数据。

### 2-23

1. vue-router 中重复点击路由会报错[NavigationDuplicated Navigating to current location](https://stackoverflow.com/questions/57837758/navigationduplicated-navigating-to-current-location-search-is-not-allowed)
2. WebGLRenderTarget 用法。
3. Int16Array

## 三月

### 3-1

1. node 读取本地配置文件，作为一个中间代理服务器，去请求接口数据。
2. 顶点着色器的值被传递到片元着色器时会进行一次插值计算。当使用`flat varying` 定义变量后，在传递时不会进行插值计算。

### 3-3

1. 材质渲染的混合模式？渲染材质时开启关闭深度模式有什么区别？

### 3-4

1. 使用物体`Line`绘制线段。

### 3-5

1. 绘制雪花的代码详解。
2. `BufferGeometry`的属性`morphAttributes`用于存储顶点变形动画，实现模型的变形和动画效果。
3. 示例代码添加注释。

### 3-19

1. `InstancedMesh`实例化网格。是一种用于实例化渲染多个相同几何体的网格的对象。它可以提高渲染性能，特别适用于需要大量重复的几何体的场景。

2. ```javascript
   const arr = [1,2,3,4,5,6];
   arr.splice(arr.indexOf(3),1);
   ```

### 3-20

1. 房谋杜断
2. `new Float32Array(4 * 3)` 是 JavaScript 中创建一个包含 12 个浮点数的新的 Float32Array 数组的语法
3. object.updateMatrix(); // 更新局部变换矩阵 object.updateMatrixWorld(); // 更新世界变换矩阵

### 3-28

1. 设置滚动条在容器上侧和左侧。[代码](https://github.com/hkp4570/daily-demo/blob/main/src/CSS%E8%AE%BE%E7%BD%AE%E6%BB%9A%E5%8A%A8%E6%9D%A1%E4%BD%8D%E7%BD%AE%E5%9C%A8%E4%B8%8A%E4%BE%A7%E5%92%8C%E5%B7%A6%E4%BE%A7/index.html)
2. jspdf 生成文件后上传到后端服务器。将 pdf 文件转换为 blob 文件，`const pdfBlob = PDF.output('blob')`

## 四月

### 4-7

1. macos 虚拟机安装。
2. github-page 页面 404。
3. x64 arm64。
4. 网站上的 cookie 设置。[为什么每个网站都要求你接受 cookie](https://zhuanlan.zhihu.com/p/569770479)
5. macos M1 芯片安装虚拟机[流程](https://zhuanlan.zhihu.com/p/452412091)。

### 4-8

1. picGo+github+typora 搭建免费图床。

   自定义域名：https://cdn.jsdelivr.net/gh/colourful96/ImagePicGo@main/img

### 4-10

1. Vue 的实例方法/生命周期。`vm.$nextTick([callback])`将回调延迟到下次 DOM 更新循环之后执行。

   [使用场景](https://blog.csdn.net/zhouzuoluo/article/details/84752280)

### 4-16

1. ThreeJS 中的局部相机。把相机添加到对象中，相机的位置和方向是相对于对象的。
2. 通过 ES6 的方式的模块化在 nodejs 中无法运行，在`package.json`文件中添加`type:module`。

### 4-17

1. 无障碍——使每个人都能使用 Web。文档阅读。
2. 使用`webpack`构建项目。如果是一个模块化项目，则需要使用相关配置。怎么打包没有引用的 css 文件？需要在入口文件中引入样式文件。

### 4-18

1. v -mode，双向数据绑定。
2. ant-design-vue 的 form 表单使用。
3. 类的继承模式。this 指向。

### 4-19

1. `Element.replaceChildren()` 用于清空 node 后代节点或者替换后代节点。
2. **`HTMLSelectElement.selectedIndex`** 是一个长整型数，它反映了被选中的第一个`option`元素的索引值。值为 -1 时表明没有元素被选中。
3. `canvas` 的方法`drawImage`。
4. threejs 中的`ImageLoader`实例。

### 4-23

1. `webpack`设置热更新。

### 4-24

1. `webpack`[监听文件变化](https://webpack.docschina.org/configuration/watch/)，文件变化后重新编译。

2. `window.matchMedia`可用于判定`document`是否匹配媒体查询？

3. 媒体查询

   ```css
   @mixin touch-vars {

   	@media (pointer: coarse) {
   		&.allow-touch-styles,
   		&.allow-touch-styles & {
   			@content;
   		}
   	}

   	&.force-touch-styles,
   	&.force-touch-styles & {
   		@content;
   	}
   }
   ```

4. 值传递和引用传递。

5. Node.insertBefore()。

### 4-25

1. [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) 值的 **`toPrecision()`** 方法返回一个以指定精度表示该数字的字符串。

### 4-26

1. **`spellcheck`** [全局属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes)是一个[枚举](https://developer.mozilla.org/zh-CN/docs/Glossary/Enumerated)属性，定义是否可以检查元素的拼写错误。对于可能包含敏感信息的元素，可以设置为`false`。

## 五月

### 5-9

1. vue 中使用 svg 时需要做其他处理。
2. `orientationchange`是移动设置上的事件，它在设备方向发生变化是触发。
3. vue 中组件过渡内置组件。

### 5-10

1. 更新 rem。

### 5-11

1. `String.fromCharCode()`对 A-Z 排序。

### 5-13

1. `figure`可附标题[内容元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/figure)。

### 5-17

1. Vue 自定义指令。 `Vue.component()`。
2. 复制内容到剪切板，兼容旧版浏览器。

### 5-20

1. 深拷贝与浅拷贝

   ```javascript
   Object.assign()
   扩展运算符
   JSON.parse(JSON.stringify())
   window.structuredClone()
   递归
   ```

### 5-21

1. 拖拽排序。

### 5-24

1. jspdf 下载 PDF，转换文件时，svg 图表转换为图片。否则图表数据丢失。

### 5-27

1. URL.createObjectURL()。
2. p 元素内不允许再包含 p 元素；语义结构，可访问性，样式和布局，标准规范。
3. echarts 中图表加载时 animationDelay 设置入场动画。

### 5-30

1. **`<hgroup>`** [HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML) 元素代表文档标题和与标题相关联的内容，它将一个 [`–`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Heading_Elements) 元素与一个或多个 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 元素组合在一起。

### 5-31

1. vue@2.6 版本和 webpack5 会有兼容性问题，导致一些 nodejs 模块不会在自动 polyfill。

## 七月

### 7-4

1. `process.args`命令行参数。`yargs-parse`包可用来格式化命令行参数。
2. `package.json`中安装的包版本控制。符号代表什么？
3. [前端路由](https://juejin.cn/post/6844903890278694919)
4. `<script>`标签中写`async defer`的区别？
5. recoil文档。
6. `nodejs`中的`event`事件。

### 7-5

1. `umijs`中配置全局样式，不必要在每个样式文件中引入全局的样式表（变量和公共样式）。

2. `typescript`中`type` 和`interface`的区别？

3. `React.ReactNode` `JSX.Element`的区别？

4. `antd`中自定义`font`图标。

   ```javascript
   import { createFromIconfontCN } from '@ant-design/icons';
   ```

5. `umi-request`源码。

### 7-9

1. 数组的`sort`方法会改变原数组，`toSorted`方法不会改变原数组。

### 7-15

1. `Express`需要通过中间件的使用`session`。
2. 地理编码，逆地理编码。[高德接口](https://developer.amap.com/api/webservice/guide/api/georegeo)

### 7-16

1. `v-html`插入html的内容。
2. `nodejs`中`crypto`加密。

### 7-17

1. `dom.innerHTML`、`dom.innerTEXT`、`dom.textContent`。

### 7-18

1. `<script type='importmap'></script>`用于定义模块导入映射。

## 十二月

### 12-5

1. 接口并发处理。
2. p-all p-queue。

### 12-6

1. 接口取消请求。
2. FileReader。
3. uni-request 配合AbortController取消请求。

### 12-9

1. npm install --legacy-peer-deps  安装包时版本有冲突。

### 12-26

1. 默认行为（仅src属性）：同步加载，阻塞HTML解析，按顺序执行。async属性：异步加载，不阻塞HTML解析，执行顺序不确定。defer属性：异步加载，不阻塞HTML解析，按顺序执行，且在HTML解析完成后执行。
2. console.log()不同格式的输出，以及格式化带样式输出。[文档](https://developer.mozilla.org/zh-CN/docs/Web/API/console)
3. declare。
4. 在子类的构造函数中，必须在使用 `this` 之前调用 `super()`，否则将会导致运行时错误。
5. ReactDOM.findDOMNode()。
6. excels。将图片放到表格中，配合html2canvas截图工具。

### 12-30

1. 普通对象和通过构造函数构造的对象的异同。
2. getPrototypeOf() 静态方法返回指定对象的原型。
3. react-is  检查特定react元素。
4. react，forwardRef  , createElement。

### 12-31

1. fs-extra  扩展fs系统的方法。
2. @monaco-editor/react  代码编辑器。

# 2025

## 一月

### 1-2

1. ```javascript
           if (event.key === 'Tab') {
               event.preventDefault();
               // 获取当前的文本框
               const textarea = event.target as HTMLTextAreaElement;
               if(textarea && textarea.tagName==='TEXTAREA'){
                   // 获取光标位置
                   const start = textarea.selectionStart;
                   const end = textarea.selectionEnd;
            
                   // 设置新的值并移动光标
                   textarea.value = textarea.value.substring(0, start)
                       + '  ' // 插入Tab符，可能需要使用空格来代替
                       + textarea.value.substring(end);
            
                   // 将光标移到Tab符之后
                   textarea.selectionStart =
                       textarea.selectionEnd = start + 1; // +1 或者根据你的制表符宽度设置
               }
               return false;
           }
   ```

### 1-3

1. macos 中执行 sh  test.sh。

### 1-14

1. 使用MutationObserver来监测DOM变化，从而知道某一个元素的子元素是否已经完全渲染完成。
2. 根据数据下载json文件。

### 1-15

1. typescript中import type{} from ''；  [import和import type](https://juejin.cn/post/7111203210542448671)

2. > 在 CSS 中，`font-weight` 属性用于设置字体的粗细。常用的数值及其对应的命名值如下：
   >
   > - `100` - Thin
   > - `200` - Extra Light (Ultra Light)
   > - `300` - Light
   > - `400` - Normal (Regular)
   > - `500` - Medium
   > - `600` - Semi Bold (Demi Bold)
   > - `700` - Bold
   > - `800` - Extra Bold (Ultra Bold)
   > - `900` - Black (Heavy)

## 二月

### 2-5

1. 全局安装typescript后可以使用tsc命令编译ts文件，局部安装可使用npx tsc。
2. Node.ownerDocument只读属性会返回当前节点的顶层的 document 对象。
3. 在浏览器中，**`document.defaultView`** 返回与[文档](https://developer.mozilla.org/zh-CN/docs/Glossary/Browsing_context)关联的 [`window`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window) 对象，如果没有可用的对象，则返回 `null`。

### 2-6

1. **`Node.cloneNode()`** 方法返回调用该方法的节点的一个副本。

2. `is` 关键字常用于自定义类型保护

   ```javascript
   export const isTextNode = (node: Node): node is Text => node.nodeType === Node.TEXT_NODE;
   ```

3. [影子DOM](https://zh.javascript.info/shadow-dom)

### 2-7

1. DOM结构中的节点包括元素节点、文本节点、注释节点。
2. document.open()  document.write()  document.close()。
3. document.adoptNode() **`Document.adoptNode()`** 将[节点（DOM）](https://developer.mozilla.org/zh-CN/docs/Glossary/Node/DOM)从另一个[文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)转移至调用该方法的文档中。被转移的节点及其子树将会从原始文档（如果存在的话）中移除，并且它们的 [`ownerDocument`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/ownerDocument) 会变更为当前文档。然后节点将被插入到当前文档中。
4. [doctype:DocumentType](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentType)
5. document.readyState 描述了document的加载状态。

### 2-8

1. dispatchEvent() 调用一个Event事件。
2. **`MouseEvent`** 接口指用户与指针设备（如鼠标）交互时发生的事件。
3. [html2canvas实现浏览器截图的原理](https://juejin.cn/post/6908255717317148685)
4. [你遇到过html2canvas的裁剪错误吗？这篇源码解析也许可以帮到你](https://juejin.cn/post/7078594967970512932?searchId=2025020811231521D5D35FF448ED4DF75E)

### 2-10

1. 按照文档配置好flow进行开发，在vs code中需要安装Flow Language Support" 插件，在项目根目录创建 .vscode/settings.json（如果还没有的话）添加以下配置：

   ```json
   {
       "javascript.validate.enable": false,
       "flow.enabled": true,
       "flow.useNPMPackagedFlow": true
   }
   ```

2. `npm publish`命令报错403，一般是名称重复。

### 2-11

1. 使用jest编写测试用例，默认不支持esm，需要下载babel插件 @babel/preset-env babel-jest使用。

### 2-13

1. 通过FileReader()和ExcelJS实现前端验证文件内容是否正确。

# lil-gui

---

1. 模块化，`.ejs`和`.mjs`，在`package.json`文件中添加`type:module`可以在`nodejs`中使用 ES6 模块化。

2. 类中的`constructor`，当创建类的实例时进行初始化操作。一个类中只能有一个`constructor`，如果子类中也定义了此方法，怎需要通过`super()`方法调用父类的`constructor`。

3. 无障碍，标签语义化。[WAI-ARIA](https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility/WAI-ARIA_basics)

4. `textContent`表示节点文本内容，与`innerText`和`innerHTML`的[区别](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent)?

5. **`CSSStyleDeclaration.setProperty()`** 方法接口为一个声明了 CSS 样式的对象设置一个新的值。

6. [CSS 自定义属性和变量](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties)。`this.domElement.style.setProperty('--width', width + 'px');`：这行代码通过 JavaScript 设置了名为 `--width` 的 CSS 变量的值为 `width + 'px'`。这里的 `width` 是一个变量，它的值会以像素（'px'）作为单位，并且被赋给 `--width` 这个自定义属性。

   通过这种方式，你可以在 CSS 中使用 `var(--width)` 来引用这个 CSS 变量，并在不同的地方灵活地使用这个值。这种做法使得你可以在 JavaScript 中动态地改变 CSS 变量的值，从而实现更灵活的样式控制。

7. 类之间的继承。在子类中调用`super()`方法是用来调用父类的构造方法。

8. `Controller`类中的`_listenCallback`方法？

9. `gui.add()`方法会返回一个`controller`实例，每个`controller`的`onchange`方法触发都会调用`gui.onChange`的方法。

10. ```javascript
    _snap( value ) {
    		const r = Math.round( value / this._step ) * this._step;
    		return parseFloat( r.toPrecision( 15 ) );
    	}
    ```

11. 监听 CSS 属性`traination`的变化

    ```javascript
    this.$children.addEventListener( 'transitionend', onTransitionEnd );
    ```
