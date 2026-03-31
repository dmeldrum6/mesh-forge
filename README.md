# mesh-forge

**A browser-based 3D object builder and OBJ exporter powered by Three.js.**

Build 3D scenes from primitives, import custom Three.js geometry, and export everything as a clean `.obj` file — no install, no build step, just open the HTML file.

![Three.js](https://img.shields.io/badge/Three.js-r128-orange?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![No dependencies](https://img.shields.io/badge/dependencies-none-blue?style=flat-square)

---
<img width="1918" height="907" alt="image" src="https://github.com/user-attachments/assets/0447194e-3a9f-4cb6-9f10-a77191aacd00" />
<img width="1917" height="909" alt="image" src="https://github.com/user-attachments/assets/c45cd2bf-da80-4cf2-9545-8ede1a72509d" />


## Features

- **Primitive shape builder** — Box, Sphere, Cylinder, Torus, Cone, and Icosahedron with live parameter controls
- **Transform panel** — Adjust position, rotation, and scale per object
- **Scene manager** — Add multiple objects to a scene, select and edit them independently
- **Color picker** — Quick color swatches for material assignment
- **Custom code import** — Paste any Three.js snippet that assigns to a `result` variable and it gets added to the scene
- **File import** — Drag and drop a `.js` or `.html` file to extract and run Three.js geometry code
- **AI prompt generator** — Built-in prompt templates to generate Three.js geometry code with Claude or ChatGPT
- **OBJ export** — Hand-rolled exporter that merges all scene geometry into a single `.obj` file, preserving transforms
- **Zero dependencies** — Single self-contained HTML file; Three.js loaded from CDN

---

## Getting Started

No installation required.

```bash
git clone https://github.com/your-username/mesh-forge.git
cd mesh-forge
open threejs-obj-exporter.html   # or just double-click it
```

The tool runs entirely in your browser. No server needed.

---

## Usage

### Building with Primitives

1. Open the **Build** tab in the left sidebar
2. Click a shape button (Box, Sphere, Cylinder, Torus, Cone, Icosahedron)
3. Adjust the shape parameters that appear below
4. Pick a color from the swatches
5. Click **Add to Scene** — the object appears in the **Scene** tab

### Transforming Objects

Select any object in the **Scene** tab to reveal its transform controls. You can adjust position (X/Y/Z), rotation, and scale independently for each object.

### Importing Custom Three.js Code

Click the **Import** button in the top bar. Your code must assign a `THREE.Group`, `THREE.Mesh`, or `THREE.BufferGeometry` to a variable called `result`:

```js
const result = new THREE.Group();

const bodyGeo = new THREE.CylinderGeometry(0.5, 0.6, 2, 16);
const bodyMat = new THREE.MeshPhongMaterial({ color: 0x888888 });
const body = new THREE.Mesh(bodyGeo, bodyMat);
result.add(body);

const topGeo = new THREE.SphereGeometry(0.5, 16, 16);
const topMat = new THREE.MeshPhongMaterial({ color: 0xaaaaaa });
const top = new THREE.Mesh(topGeo, topMat);
top.position.y = 1.25;
result.add(top);
```

> Code runs locally in your browser. Only the `THREE` namespace is in scope — no imports, no render loops, no scene setup.

### Using the AI Prompt Generator

Inside the Import modal, switch to the **Prompt** tab. Enter a subject (e.g. `"rocket ship"`) and click **Generate Prompt** to get a ready-made prompt you can paste into Claude, ChatGPT, or any other AI assistant. The generated code can then be pasted straight back into the code import box.

### Exporting to OBJ

Once you have objects in your scene, the **Export OBJ** button in the Scene panel becomes active. Click it to download `model.obj`. The exporter:

- Merges all scene objects into a single geometry
- Applies each object's position, rotation, and scale transforms
- Outputs standard Wavefront OBJ format compatible with Blender, Maya, Cinema 4D, and most 3D tools

---

## Code Import Rules

| Variable type | Behaviour |
|---|---|
| `THREE.Group` | Each child mesh becomes a separate scene object |
| `THREE.Mesh` | Added directly as a single scene object |
| `THREE.BufferGeometry` | Auto-wrapped in a `MeshPhongMaterial` mesh |

Materials are preserved for the live preview but normalized to `MeshPhongMaterial` for OBJ export compatibility.

---

## Tech Stack

| | |
|---|---|
| **Renderer** | [Three.js r128](https://threejs.org/) via CDN |
| **Fonts** | JetBrains Mono, Syne (Google Fonts) |
| **Export format** | Wavefront OBJ (hand-rolled, no plugins) |
| **Runtime** | Vanilla JS — no bundler, no framework |

---

## File Structure

```
mesh-forge/
└── threejs-obj-exporter.html   # The entire application (single file)
```

---

## Browser Compatibility

Works in any modern browser that supports WebGL. Tested in Chrome, Firefox, and Safari.

---

## License

MIT — see [LICENSE](LICENSE) for details.
