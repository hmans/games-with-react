# Reactive Gamedev

## What is it?

Reactive Gamedev is about making games using JavaScript, React and related web development technologies. This document aims at describing the stack, explaining why we think it's great, but also detailing existing challenges that we still need to tackle. Let's go! 🚀

## The Building Blocks

For game development, you may be used to thinking in terms of _engines_. Here, instead of think of _stacks_ of different libraries and tools, similar to how any other web applications are built. The stack described in this document revolves around the following components:

- [React], for expressing application structure and logic as components and functions.
- [Three.js], for managing a 3D scene powered by WebGL.
- [react-three-fiber], often just called r3f, for providing a React layer for Three.js.
- [Vite](https://vitejs.dev/) and [CRA](https://reactjs.org/docs/create-a-new-react-app.html), for enabling super-fast iteration thanks to hot-module replacement.

Work in progress libraries:

- [Miniplex](https://github.com/hmans/miniplex), a game entity manager based on ECS architecture.
- [Controlfreak](https://github.com/hmans/controlfreak), composable game input.
- Instanza
- Ingrid

## Challenges

_TODO_

- A lot of moving parts
- No (painless) path towards consoles

## Where to go next

_TODO_

- Poimandres Discord, #game-dev

[three.js]: https://threejs.org/
[react]: https://reactjs.org/
[react-three-fiber]: https://github.com/pmndrs/react-three-fiber
