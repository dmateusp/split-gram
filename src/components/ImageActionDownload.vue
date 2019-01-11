<template>
  <div id="download">
    <a class="button" @click="$_downloadImage">Download</a>
    <canvas></canvas>
  </div>
</template>

<script>
export default {
  name: 'ImageActionDownload',
  methods: {
    $_downloadImage () {
      const splitImages = this.$_splitImage(this.$parent.image, this.$parent.INSTAGRAM_IMAGE_WIDTH)
      console.log(splitImages)
    },
    $_splitImage (image, newWidth) {
      const canvas = document.createElement('canvas')
      const ctx = canvas.getContext('2d')
      canvas.width = image.naturalWidth
      canvas.height = image.naturalHeight

      ctx.drawImage(image, 0, 0, image.naturalWidth, image.naturalHeight)
      document.body.appendChild(canvas)
      return canvas.toDataURL()
    }

  }
}
</script>
