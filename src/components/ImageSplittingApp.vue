<template>
  <div id="image-component">
    <ImageSlideShow :images-split="imagesSplit" :current-index="currentIndex" @selectIndex="selectIndex" v-if="imagesSplit.length > 0"/>
    <ul>
        <li><ImageSplittingDownload :images-split="imagesSplit" :current-index="currentIndex" v-if="imagesSplit.length > 0"/></li>
        <li><ImageSplittingUpload @createSlideShow="createSlideShow"/></li>
    </ul>
  </div>

</template>

<script>
import ImageSplittingUpload from '@/components/ImageSplittingUpload'
import ImageSplittingDownload from '@/components/ImageSplittingDownload'
import ImageSlideShow from '@/components/ImageSlideShow'

export default {
  name: 'ImageActions',
  components: {
    'ImageSplittingUpload': ImageSplittingUpload,
    'ImageSplittingDownload': ImageSplittingDownload,
    'ImageSlideShow': ImageSlideShow
  },
  methods: {
    $_loadImage (imageSrc, imageName, onload) {
      const img = new Image()
      img.src = imageSrc
      img.className = 'image-width-browser'
      this.image = img
      this.imageName = imageName
      img.addEventListener('load', onload, false)
    },
    $_computeSplits (originalWidth, newWidth) {
      const numberOfSplits = Math.ceil(originalWidth / newWidth)
      const widthPerSplit = Math.ceil(originalWidth / numberOfSplits)
      return {numberOfSplits: numberOfSplits, widthPerSplit: widthPerSplit}
    },
    $_splitImageInCanvas (image, numberOfSplits, widthPerSplit) {
      return [...Array(numberOfSplits).keys()].map(
        (i) => {
          const canvas = document.createElement('canvas')
          const ctx = canvas.getContext('2d')
          const cropHeight = (image.naturalHeight - widthPerSplit)
          canvas.height = image.naturalHeight - cropHeight
          canvas.width = widthPerSplit

          ctx.drawImage(image, i * widthPerSplit, cropHeight / 2, widthPerSplit, image.naturalHeight, 0, 0, widthPerSplit, image.naturalHeight)
          const data = canvas.toDataURL('image/jpeg')
          canvas.remove()
          const imgName = this.imageName.replace(/\.[^/.]+$/, '') + '_split-gram_part-' + (i + 1) + '.jpg'
          return {name: imgName, data: data}
        }
      )
    },
    $_splitImage () {
      const {numberOfSplits, widthPerSplit} = this.$_computeSplits(this.image.naturalWidth, this.image.naturalHeight)
      return this.$_splitImageInCanvas(this.image, numberOfSplits, widthPerSplit)
    },
    createSlideShow (imageSrc, imageName) {
      const context = this
      this.$_loadImage(imageSrc, imageName, function () { context.imagesSplit = context.$_splitImage() })
    },
    selectIndex (index) {
      this.currentIndex = index
    }
  },
  data: function () {
    return {
      image: null,
      imageName: null,
      imagesSplit: [],
      currentIndex: 0
    }
  }
}
</script>

<style scoped>
ul {
  padding: 0;
  list-style-type: none;
}

li {
  text-align: center;
}
#image-component {
  max-width: 400px;
  margin: auto;
}
</style>
