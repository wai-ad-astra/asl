<template>
  <div class="uploadForm">
    <h1>{{ msg }}</h1>
<!--    when user selects new file-->
    <input type="file"  @change="onFileSelected(im, $event)">
  </div>
</template>

<script>
export default {
  name: 'UploadForm',
  props: {
    msg: String,
    im: Image
  },
  methods: {
    onFileSelected(item, e){
      const files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(item, files[0]);
      console.log(event);
    },
    createImage(item, file) {
      // const image = new Image();
      const reader = new FileReader();
      reader.onload = (e) => {
        item.im = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage(item) {
      item.im = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
