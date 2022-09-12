<script >
import { defineComponent } from 'vue'
import * as THREE from 'three'

export default defineComponent({
  mounted() {
    this.initThree();
  },
  methods: {
    initThree() {
      const scene = new THREE.Scene();

      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

      const canvas = document.querySelector('#scene');
      const renderer = new THREE.WebGLRenderer({
        canvas,
      });

      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(window.innerWidth, window.innerHeight);
      camera.position.setZ(30);

      renderer.render(scene, camera);

      const geometry = new THREE.TorusGeometry(10, 3, 16, 100)

      const material = new THREE.MeshBasicMaterial({ color: 0xFF6347, wireframe: true });

      const torus = new THREE.Mesh(geometry, material);

      scene.add(torus)

      function animate() {
        torus.rotation.x += 0.01;
        torus.rotation.y += 0.005;
        torus.rotation.y += 0.01;
        requestAnimationFrame(animate);
        renderer.render(scene, camera);
      }

      animate();
    }
  }
})
</script>

<template>
  <canvas id="scene"></canvas>
</template>

<style scoped>
canvas {
  position: absolute;
  left: 0;
  width: 100vw;
  height: 100vh;
}
</style>
