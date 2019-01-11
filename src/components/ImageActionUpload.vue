<template>
  <div id="drop-area"
       ref="dropArea"
       @dragenter.stop.prevent="$_highlight"
       @dragover.stop.prevent="$_highlight"
       @dragleave.stop.prevent="$_unhighlight"
       @drop.stop.prevent="$_handleDrop">
    <form class="my-form">
      <p>Drag image you want to split here</p>
      <input type="file" id="fileElem" accept="image/*" @change="$_handleUploadButton">
      <label class="button" for="fileElem">Browse..</label>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ImageActionUpload',
  methods: {
    $_highlight () { this.$refs.dropArea.classList.add('highlight') },
    $_unhighlight () { this.$refs.dropArea.classList.remove('highlight') },
    $_loadImage (imageData) {
      const reader = new FileReader()
      const parent = this
      reader.onload = function (e) { parent.$emit('changeImage', reader.result) }
      reader.readAsDataURL(imageData)
    },
    $_handleDrop (e) {
      this.$_unhighlight()
      this.$_loadImage(e.dataTransfer.files[0])
    },
    $_handleUploadButton (e) {
      this.$_loadImage(e.srcElement.files[0])
    }
  }
}
</script>

<style scoped>
#drop-area {
  border: 2px dashed #ccc;
  border-radius: 20px;
  width: 480px;
  font-family: sans-serif;
  margin: 100px auto;
  padding: 20px;
}
#drop-area.highlight {
  border-color: darkgray;
}
p {
  margin-top: 0;
}
.my-form {
  margin-bottom: 10px;
}
#fileElem {
  display: none;
}
</style>
