# Les fondamentaux de Three.js

Three.js est une bibliothèque JavaScript qui simplifie l’utilisation de **WebGL**, permettant de créer et afficher des **scènes 3D dans un navigateur** sans avoir à écrire tout le code bas niveau de WebGL.

---

## 🌐 1. Initialisation de base

### Concepts clés :

* **Scène (`THREE.Scene`)** : l’espace où sont placés les objets.
* **Caméra (`THREE.PerspectiveCamera`)** : permet de "voir" la scène.
* **Rendu (`THREE.WebGLRenderer`)** : affiche la scène à l’écran.

### Exemple :

```html
<!DOCTYPE html>
<html>
  <head><title>Three.js Basic</title></head>
  <body>
    <script src="https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.min.js"></script>
    <script>
      // Création de la scène
      const scene = new THREE.Scene();

      // Création de la caméra
      const camera = new THREE.PerspectiveCamera(
        75, window.innerWidth / window.innerHeight, 0.1, 1000
      );

      // Création du moteur de rendu
      const renderer = new THREE.WebGLRenderer();
      renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(renderer.domElement);

      // Création d’un cube
      const geometry = new THREE.BoxGeometry();
      const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
      const cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      camera.position.z = 5;

      // Animation
      function animate() {
        requestAnimationFrame(animate);
        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;
        renderer.render(scene, camera);
      }

      animate();
    </script>
  </body>
</html>
```

---

## 🧱 2. Objets 3D (Mesh)

### Concepts :

* **Géométries** : formes (cube, sphère, plan…).
* **Matériaux** : apparence de l’objet (couleur, texture, transparence…).
* **Mesh** : combinaison géométrie + matériau.

### Exemples :

```js
const sphere = new THREE.Mesh(
  new THREE.SphereGeometry(1, 32, 32),
  new THREE.MeshStandardMaterial({ color: 0xff0000 })
);
scene.add(sphere);
```

---

## 🔦 3. Lumières

Les lumières sont nécessaires pour voir les objets si on utilise des matériaux non basiques.

### Types :

* `THREE.AmbientLight` : lumière uniforme.
* `THREE.PointLight` : lumière ponctuelle.
* `THREE.DirectionalLight` : comme le soleil.

### Exemple :

```js
const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
scene.add(ambientLight);

const pointLight = new THREE.PointLight(0xffffff, 1);
pointLight.position.set(5, 5, 5);
scene.add(pointLight);
```

---

## 🎥 4. Caméra et contrôles

### Types de caméras :

* `PerspectiveCamera` : comme un œil humain.
* `OrthographicCamera` : sans perspective (utile pour plans techniques).

### Contrôles :

Utilise `OrbitControls` (module à importer séparément).

```html
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/controls/OrbitControls.js"></script>
```

```js
const controls = new THREE.OrbitControls(camera, renderer.domElement);
```

---

## 🎨 5. Textures et matériaux avancés

Tu peux charger des images comme textures :

```js
const texture = new THREE.TextureLoader().load('texture.jpg');
const material = new THREE.MeshStandardMaterial({ map: texture });
```

---

## 📦 6. Chargement de modèles 3D

Avec `GLTFLoader` :

```html
<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/examples/js/loaders/GLTFLoader.js"></script>
```

```js
const loader = new THREE.GLTFLoader();
loader.load('model.gltf', function(gltf) {
  scene.add(gltf.scene);
});
```

---

## 🔄 7. Animation

Animation par rotation ou déplacement :

```js
function animate() {
  requestAnimationFrame(animate);
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}
```

Ou avec un **mixer** pour les modèles `.glb/.gltf` animés.

---

## 📁 8. Organisation recommandée

Pour un projet plus grand :

* `index.html`
* `main.js`
* `scene/`, `models/`, `textures/`, etc.

---

## 📚 Ressources utiles

* Site officiel : [https://threejs.org](https://threejs.org)
* Playgrounds : [https://threejs.org/editor](https://threejs.org/editor), [CodeSandbox](https://codesandbox.io/)
* Modèles gratuits : [https://sketchfab.com](https://sketchfab.com), [https://poly.pizza](https://poly.pizza)

---
