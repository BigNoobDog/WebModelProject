<template>
  <div id="app"></div>
</template>

<script>
import * as THREE from "three";
import { WEBGL } from "./js/webgl";

export default {
  methods: {
    init() {
      //初始化

      if (WEBGL.isWebGLAvailable() === false) {
        this.document.body.appendChild(WEBGL.getWebGLErrorMessage());
      }
      // console.log(THREE);
      // var textrueUrl = this.getTexture("baseColor");
      // console.log("name=%s", textrueUrl);

      this.testScene();
    },

    testScene() {
      this.camera = new THREE.PerspectiveCamera(
        70,
        window.innerWidth / window.innerHeight,
        0.01,
        10
      );
      this.camera.position.z = 1;

      this.scene = new THREE.Scene();

      var geometry = new THREE.BoxGeometry(0.2, 0.2, 0.2);
      var material = new THREE.MeshNormalMaterial();

      this.mesh = new THREE.Mesh(geometry, material);
      this.scene.add(this.mesh);

      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(window.innerWidth, window.innerHeight);

      this.$el.appendChild(this.renderer.domElement);
      this.animate();
    },
    animate() {
      requestAnimationFrame(this.animate);

      this.mesh.rotation.x += 0.01;
      this.mesh.rotation.y += 0.02;

      this.renderer.render(this.scene, this.camera);
    },
    getTexture(name) {
      var textures = {
        baseColor: { url: "textures/6414/ambientOcclusion.png" },
        metallic: { url: "textures/6414/metallic.png" },
        normal: { url: "textures/6414/normal.png" },
        roughness: { url: "textures/6414/roughness.png" },
        ambientOcclusion: { url: "textures/6414/ambientOcclusion.png" }
      };

      var texture = textures[name].textures;

      // if (!texture) {
      //   texture = textures[name].texture = new THREE.TextureLoader().load(
      //     textures[name].url
      //   );
      //   texture.wrapS = texture.wrapT = THREE.RepeatWrapping;

      //   library[texture.uuid] = texture;
      // }
      return texture;
    }
  },
  mounted() {
    this.init();
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
