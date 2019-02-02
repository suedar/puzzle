<template>
  <div class="main">
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->

  </div>
</template>

<script>
// @ is an alias to /src
import * as THREE from 'three';
import {SceneUtils} from '../model/js/utils/SceneUtils.js';
export default {
  name: 'home',
  components: {
  },
  data() {
    return {
      cube: '',
      camera: '',
      scene: '',
      renderer: ''
    }
  },
  methods: {
    initThree() {
      // 场景
      let scene = new THREE.Scene();
      let camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
      let renderer = new THREE.WebGLRenderer();

      renderer.setSize( window.innerWidth, window.innerHeight );
      renderer.setClearColor('#f2f2f2',1.0);

      document.body.appendChild( renderer.domElement );

      this.camera = camera;
      this.renderer = renderer;
      this.scene = scene;
    },
    initCube() {
      // 以下为旋转方块
      let group = new THREE.Group();
      this.scene.add( group );
      group.updateMatrixWorld( true ); // 更改全局变换

      let geometry = new THREE.BoxGeometry( 1, 1, 1 );
      let material = new THREE.MeshBasicMaterial( { color: '#f7d9aa' } );
      let cube = new THREE.Mesh( geometry, material );

      group.add( cube );

      let edges = new THREE.EdgesGeometry( geometry );
      let line = new THREE.LineSegments( edges, new THREE.LineBasicMaterial( { color: 0xffffff } ) );

      group.add( line );

      let circleGeometry = new THREE.CircleGeometry( 5, 8, 1);
      let circleMaterial = new THREE.MeshBasicMaterial( { color: 0xffff00 } );
      let circle = new THREE.Mesh( circleGeometry, circleMaterial );
      // group.add( circle );

      this.scene.add(group);

      this.camera.position.z = 5;

      this.cube = group;
    },
    createChip() {
      
    },
    createGe() {
    },
    initBg() {

    },
    animate() {
        requestAnimationFrame( this.animate );
        this.cube.rotation.x += 0.01;
        this.cube.rotation.y += 0.01;
        this.renderer.render( this.scene, this.camera );
    },
    Sea() {
      // 创建一个圆柱几何体
      // 参数为：顶面半径，底面半径，高度，半径分段，高度分段
      var geom = new THREE.CylinderGeometry(600,600,800,40,10);

      // 在 x 轴旋转几何体
      geom.applyMatrix(new THREE.Matrix4().makeRotationX(-Math.PI/2));

      // 创建材质
      var mat = new THREE.MeshPhongMaterial({
          color: '#2f2',
          transparent:true,
          opacity:.6,
          shading:THREE.FlatShading,
      });

      // 为了在 Three.js 创建一个物体，我们必须创建网格用来组合几何体和一些材质
      this.mesh = new THREE.Mesh(geom, mat);

      // 允许大海对象接收阴影
      this.mesh.receiveShadow = true;
    }
  },
  created() {
    this.initThree();
    this.initCube();
    this.animate();
    this.createGe();
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
    .main {
      // background: linear-gradient(#e4e0ba, #f7d9aa);
      // background: #ddd;
      // width: 100vw;
      // height: 100vh;
    }
    canvas {
      background-color: #e4e0ba;
      position: absolute;
      width: 100%;
      height: 100%;
      overflow: hidden;
    }
  }

</style>

