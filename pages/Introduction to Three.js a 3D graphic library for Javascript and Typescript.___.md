- Three.js is a 3D graphics library for web. You can use Javascript and Typescript.
- It's a powerful library that allows you showcase 3D objects to the user and even make 3D games.
- Here's how you can install it. I assume you're using NPM and Vite.
-
- ```bash
  npm add three
  ```
-
- And if you use typescript, install the type too.
-
- ```bash
  npm add --save-dev @types/three
  ```
-
- Now we're going to open our typescript file, create one if you haven't. The next thing is simply to understand that in 3D we need to have a `Scene`, `Camera`, `Object`, and optionally `Light`. Those things are the fundamentals we can think of logically without memorize them manually, because those things exists in real life. And lastly we need `Renderer`. A renderer needs camera and will render our 3d scene to our 2d screen. Pretty straightforward, right? Here's an example.
-
- ```typescript
  import * as THREE from "three";
  
  // first we need a scene.
  const scene = new THREE.Scene();
  
  // setup camera.
  const camera = new THREE.PerspectiveCamera();
  
  // our object is a simple box. I'll explain this line later.
  const obj = new THREE.Mesh(new THREE.BoxGeometry(), new THREE.MeshBasicMaterial());
  
  // then add everything to the scene.
  scene.add(camera, light, obj);
  ```
-
- If we run this program, it won't render anything because... we don't have a renderer!
- So we setup a renderer and we will take the scene and the camera.
-
- ```typescript
  // setup the renderer.
  const renderer = new THREE.WebGLRenderer();
  
  // render our scene from the camera's perspective.
  renderer.render(scene, camera);
  ```
-
- Now should render our scene.
-
- **What is a mesh?**
- Take a look at this code.
-
- ```typescript
  const obj = new THREE.Mesh(new THREE.BoxGeometry(), new THREE.MeshBasicMaterial());
  ```
-
- Our mesh takes `BoxGeometry` and `MeshBasicMaterial`.
- Box geometry is a vertices data that made up a box.
- Mesh basic material is a material for our mesh, like color.
- Mesh is a wrapper around those geometry data and a material.
- Look at this code.
-
- ```typescript
  // you can even setup a custom vertices to your geometry.
  // here are some of the predefined geometry threejs has.
  const geometry = new THREE.BoxGeometry(); // box vertices
  const geometry1 =  new THREE.ConeGeometry(); // cone vertices
  const geometry2 = new THREE.SphereGeometry(); // sphere vertices
  
  const material = new THREE.MeshBasicMaterial({
    color: THREE.Color.NAMES.blue,
  }); // our material with color blue.
  
  // our mesh is a wrapper around those things and make it a 3d mesh.
  const object = new THREE.Mesh(geometry, material);
  ```
-
- We need to set the camera position too.
-
- ```typescript
  camera.position.z = 5;
  ```
-
- And we also need to place our render call inside a animation loop, so it runs multiple times per seconds usually 60 FPS depends on our monitor refresh rate.
-
- ```diff
  - renderer.render(scene, camera);
  + function loop() {
  +   renderer.render(scene, camera);
  + }
  + renderer.setAnimationLoop(loop);
  ```
-
- There are also helpers in threejs module that you can use to help you navigate/visualize your intention. Like grid helper, orbit controls, transform controls, and many others.
-
- This orbit controls help you move around the camera in your scene, with your mouse.
-
- ```typescript
  import { OrbitControls } from "three/addons";
  
  const controls = new OrbitControls(camera, renderer.domElement);
  
  // need to call update for every manual camera transformation like camera.position.z = x
  controls.update();  
  ```
-
- There is also grid helper. Which adds a grid to the scene.
-
- ```typescript
  const grid = new THREE.GridHelper();
  scene.add(grid);
  ```
-
-
- **Sources: **
- https://threejs.org/manual/pages/installation.html
- https://threejs.org/docs/#OrbitControls
-
-
- #threejs #web #javascript #typescript #3d
-