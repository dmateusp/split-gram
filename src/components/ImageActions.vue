<template>
  <div id="image-component">
    <div ref="image"/>
    <ul>
        <li><ImageActionUpload @changeImage="$_changeImage"></ImageActionUpload></li>
        <li><ImageActionDownload></ImageActionDownload></li>
    </ul>
  </div>

</template>

<script>
import ImageActionUpload from '@/components/ImageActionUpload'
import ImageActionDownload from '@/components/ImageActionDownload'

export default {
  name: 'ImageActions',
  components: {
    'ImageActionUpload': ImageActionUpload,
    'ImageActionDownload': ImageActionDownload
  },
  methods: {
    $_changeImage (imageSrc) {
      const img = new Image()
      img.src = imageSrc
      this.image = img

      img.width = this.INSTAGRAM_IMAGE_WIDTH

      if (this.$refs.image.firstChild != null) {
        this.$refs.image.removeChild(this.$refs.image.firstChild)
      }
      this.$refs.image.appendChild(img)
    }
  },
  data: function () {
    return {
      image: null,
      INSTAGRAM_IMAGE_WIDTH: 1080
    }
  }
}
</script>

<style>
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
