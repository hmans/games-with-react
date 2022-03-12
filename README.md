# Reactive Gamedev

## What is it?

Reactive Gamedev is about making games using JavaScript, React and related web development technologies. This document aims at describing the stack, explaining why we think it's great, but also detailing existing challenges that we still need to tackle. Let's go! 🚀

## The Building Blocks

### React

React, which you have very likely already heard of, is the massively popular JavaScript library that describes itself as:

> A JavaScript library for building user interfaces

If you're a web developer, chances are good that you've worked with React or any of the countless similarly-minded frameworks (like Vue, Svelte, SolidJS et al) before. Most people use it to build HTML-based web applications with it, and it allows them to encapsulate both view and application logic into reusable, composable and shareable components like this:

```jsx
const User = ({ name, email }) => (
  <p>
    <a href={"mailto:" + email}>{name}</a>
  </p>
);

const Users = () => {
  const users = useMemo(loadUsers);

  return (
    <div className="users">
      {users.map((user) => (
        <User key={user.id} name={user.name} email={user.email} />
      ))}
    </div>
  );
};
```

### Three.js

[Three.js] is a JavaScript wrapper around WebGL, WebGL2 and (soon) WebGPU. It is absolutely not the only library of its kind, but it is easily the most popular one.

Three.js offers an [object-oriented, imperative API](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene) for constructing and managing 3D scenes:

```js
/* Create a scene */
const scene = new THREE.Scene();

/* Create a camera */
const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
camera.position.z = 5;

/* Create a renderer */
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

/* Add a cube to the scene */
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

/* Animate the scene */
function animate() {
  requestAnimationFrame(animate);

  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;

  renderer.render(scene, camera);
}

animate();
```

### react-three-fiber

react-three-fiber, often just called r3f, is a library for React that extends the JSX syntax with elements that manage a Three.js scene for you. A simple, non-animated react-three-fiber version of the example above might look like this:

```jsx
const App = () => {
  return (
    <Canvas camera={{ position: [0, 0, 5] }}>
      <mesh>
        <boxGeometry />
        <meshBasicMaterial color="#00ff00" />
      </mesh>
    </Canvas>
  );
};
```

react-three-fiber essentially translates the given tags (`meshBasicMaterial`) to the Three.js class name counterparts (`THREE.MeshBasicMaterial`), creates an instance of that class, assigns the given properties (like `color`), and then automatically assigns them to the parent's corresponding property (in this case, `mesh.material`.)

For managing and animating your scene, you will use a mix of the standard React tooling and hooks provided by react-three-fiber:

```jsx
const App = () => {
  /* useRef is a React hook that provides an object that lets us store a reference to an element we have rendered. See the <mesh> element below! */
  const cube = useRef();

  /* useFrame will execute the given function once per frame */
  useFrame(() => {
    cube.current.rotation.x += 0.01;
    cube.current.rotation.y += 0.01;
  });

  return (
    <Canvas camera={{ position: [0, 0, 5] }}>
      <mesh ref={cube}>
        <boxGeometry />
        <meshBasicMaterial color="#00ff00" />
      </mesh>
    </Canvas>
  );
};
```

Using React and react-three-fiber offers a number of advantages over writing imperative Three.js code:

- A declarative development model: scene objects and logic that manages them are implemented within cleanly encapsulated components and functions that you can then assemble declaratively using JSX. This goes a long way in making the various bits and bobs of your game reusable, testable, and just generally easier to reason about.
- Automatic resource management: in imperative Three.js code, a non-trivial part of your work is to deal with creating and disposing of the resources used in your scene, starting from actual scene objects (like the cube) to WebGL resources they need (like materials and geometries), the latter being especially tricky since they're [not necessarily cleaned up as automatically as you might expect](https://threejs.org/docs/#manual/en/introduction/How-to-dispose-of-objects). react-three-fiber will do a large part of this work for you.
- Benefiting from React tooling: React offers a huge ecosystem of existing tooling that you can use in your game, from state management libraries to bundlers providing hot-reloading of updated code through HMR.

### ECS

_TODO_

### Vite & CRA

_TODO_

## Challenges

_TODO_

- A lot of moving parts
- No (painless) path towards consoles

## Where to go next

_TODO_

- Poimandres Discord, #game-dev

[three.js]: https://threejs.org/
