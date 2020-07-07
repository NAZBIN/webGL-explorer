<template>
  <div id="container"></div>
</template>

<script>
import * as Three from "three";
// import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader"; //引入一个加载器

export default {
  name: "ThreeTest",
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null,
    };
  },
  methods: {
    init: function() {
      let container = document.getElementById("container");
      this.scene = new Three.Scene();
      this.camera = new Three.PerspectiveCamera(
        30,
        container.clientWidth / container.clientHeight,
        0.1,
        10
      );
      this.camera.position.z = 1;
      this.renderer = new Three.WebGLRenderer({ antialias: true }); //渲染器

      let geometry = new Three.BoxGeometry(0.2, 0.2, 0.2);
      let material = new Three.MeshNormalMaterial(); //选择材质

      this.cube = new Three.Mesh(geometry, material);
      this.scene.add(this.cube);

      this.renderer.setSize(
        container.clientWidth,
        container.clientHeight,
        false
      ); //第三个参数设置为false 将以较低的分辨率来呈现
      container.appendChild(this.renderer.domElement);
    },
    animate: function() {
      requestAnimationFrame(this.animate);
      this.cube.rotation.x += 0.01;
      this.cube.rotation.y += 0.02;
      this.renderer.render(this.scene, this.camera);
    },
  },
  mounted() {
    this.init();
    this.animate();
  },
};
</script>

<style scoped>
#container {
  width: 500px;
  height: 500px;
}
</style>
