<template>
  <div class="ImageDisplay">
    <h1>{{ imName }}</h1>
<!--    when user selects new file-->
    <div v-if="im">
      <img :src="im" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageDisplay',
  props: {
    imName: String,
    im: Image
  },
  methods: {
    onFileSelected(item, event){

      console.log(event);
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
