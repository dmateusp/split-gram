<template>
  <div>
    <div id="drop-area"
       ref="dropArea"
       @dragenter.stop.prevent="$_highlight"
       @dragover.stop.prevent="$_highlight"
       @dragleave.stop.prevent="$_unhighlight"
       @drop.stop.prevent="$_handleDrop">
    <form class="upload-image-form">
      <p>Drag image you want to split here</p>
      <input type="file" id="fileElem" accept="image/*" @change="handleUploadButton">
      <label class="button" for="fileElem">Browse..</label>
    </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageSplittingUpload',
  methods: {
    $_highlight () { this.$refs.dropArea.classList.add('highlight') },
    $_unhighlight () { this.$refs.dropArea.classList.remove('highlight') },
    $_loadImage (imageData) {
      const reader = new FileReader()
      const parent = this
      reader.onload = function (e) { parent.$emit('createSlideShow', reader.result, imageData.name) }
      reader.readAsDataURL(imageData)
    },
    $_handleDrop (e) {
      this.$_unhighlight()
      this.$_loadImage(e.dataTransfer.files[0])
    },
    handleUploadButton (e) {
      this.$_loadImage(e.srcElement.files[0])
    }
  }
}
</script>

<style scoped>
* {box-sizing:border-box}

#drop-area {
  border: 2px dashed #ccc;
  border-radius: 10px;
  font-family: sans-serif;
  margin: 50px auto;
  width: 80%;
  padding: 20px;
}
#drop-area.highlight {
  border-color: darkgray;
}
p {
  margin-top: 0;
}
.upload-image-form {
  margin-bottom: 10px;
}
#fileElem {
  display: none;
}
.button {
  display: inline-block;
  padding: 10px;
  background: #ccc;
  cursor: pointer;
  border-radius: 5px;
  border: 1px solid #ccc;
}
.button:hover {
  background: #ddd;
}
</style>
