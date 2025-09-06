[youtube](ttps://www.youtube.com/watch?v=-T6EbWCq99c&list=PLPbmjY2NVO_X1U1JzLxLDdRn4NmtxyQQo)

# 三個最基本的東西
	1. HTML canvas element
	2. WebGL rendering context(gl)
	3. WebGl programming linking to compiled shaders

```js
const gl = canvas.getContext('webgl2');
```

# Create a WebGLProgram

```js
const program = gl.createProgram();
... // do shader things
gl.useProgram(program);
```

# 建立兩種Shader
## VertexShader and FragmentShader

```js
// 1. create by type, gl.VERTEX_SHADER or gl.FRAGMENT_SHADER
const shader = gl.createShader(type);

// 2. set source, 一段GLSL語言
gl.shaderSource(shader, source);

// 3. compile
gl.compileShader(shader);

// attach
gl.attachShader(program, vertexShader);
gl.attachShader(program, fragmentShader);
gl.linkProgram(program);
const success = gl.getProgramParameter(program, gl.LINK_STATUS);


```