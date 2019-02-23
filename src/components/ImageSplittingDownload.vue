<template>
  <div class="container">
    <a class="button" :href="imagesSplit[currentIndex].data" :download="imagesSplit[currentIndex].name" target="_blank">Download</a>
  </div>
</template>

<script>
export default {
  name: 'ImageSplittingDownload',
  props: {
    imagesSplit: Array,
    currentIndex: Number
  }
}
</script>

<style scoped>
* {box-sizing:border-box}

.container {
  width: 100%;
}
.button {
  display: inline-block;
  padding: 10px;
  background: #ccc;
  cursor: pointer;
  border-radius: 5px;
  border: 1px solid #ccc;
  text-decoration: none;
  color: black;
}
.button:hover {
  background: #ddd;
}
</style>
