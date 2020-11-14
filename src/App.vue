<template>
  <div id="app">
    <img alt="ASL logo" src="./assets/ASL.png">
    <div>
      <video ref="video" id="video" width="640" height="480" autoplay></video>
    </div>
    <div>
      <button id="snap" v-on:click="capture()">Snap Photo</button>
    </div>
    <canvas ref="canvas" id="canvas" width="640" height="480"></canvas>
    <ul>
      <li v-for="(c, i) in captures" :key="i">
        <img v-bind:src="c" height="50"/>
      </li>
    </ul>
  </div>
</template>

<script>
// import UploadForm from './components/UploadForm'
// import ImageDisplay from "@/components/ImageDisplay";
import * as tf from '@tensorflow/tfjs';

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      video: {},
      canvas: {},
      captures: [],
      model: {},
    }
  },
  methods: {
    capture() {
      this.canvas = this.$refs.canvas;
      this.canvas.getContext("2d").drawImage(this.video, 0, 0, 640, 480);
      this.captures.push(this.canvas.toDataURL("image/png"));
    }
  },
  async mounted() {
    console.log('hi')
    this.video = this.$refs.video;
    if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
      navigator.mediaDevices.getUserMedia({video: true}).then(stream => {
        this.video.srcObject=stream;
        this.video.play();
        // deprecated
        // this.video.src = window.URL.createObjectURL(stream);
      });
    }
    //  Load model
    // this.model = await tf.loadLayersModel('https://foo.bar/tfjs_artifacts/model.json');
    // console.log(this.model);
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: #F0F0F0;
}

#video {
  background-color: #000000;
}

#canvas {
  display: none;
}

li {
  display: inline;
  padding: 5px;
}
</style>
