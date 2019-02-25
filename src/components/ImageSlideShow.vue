<template>
  <div ref="slideshowContainer">
    <tiny-slider class="slideshow-container" @transitionEnd="$_selectIndex" :mouse-drag="true" :touch="true" :loop="false" :controls="false" :nav="false" items="1">
        <div :class="(index === 0) ? 'split-slides' : 'split-slides hidden'" :key="index" v-for="(image, index) of imagesSplit">
          <img :src="image.data" :id="image.name" class="image-width-browser"/>
        </div>
    </tiny-slider>
    <div id="dots">
      <div id="dot" :key="index" v-for="index in imagesSplit.length">
        <span class="dot-selected" v-if="index - 1 == currentIndex"></span>
        <span class="dot" v-else></span>
      </div>
    </div>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/tiny-slider/2.3.5/tiny-slider.css"/>
  </div>
</template>

<script>
import VueTinySlider from 'vue-tiny-slider'

export default {
  name: 'ImageSlideShow',
  methods: {
    $_replaceImage (elem) {
      if (this.$refs.slideshowContainer.firstChild != null) {
        this.$refs.slideshowContainer.removeChild(this.$refs.slideshowContainer.firstChild)
      }
      this.$refs.slideshowContainer.appendChild(elem)
    },
    $_selectIndex (info) {
      this.$emit('selectIndex', info.displayIndex - 1)
    }
  },
  props: {
    imagesSplit: Array,
    currentIndex: Number
  },
  components: {
    'tiny-slider': VueTinySlider
  }
}
</script>

<style scoped>

.image-width-browser {
  width: 100%;
  max-height: 600px;
}

.slideshow-container {
  width: 100%;
  position: relative;
  margin: auto;
}

.hidden {
  display: none;
}
#dot {
  display: inline-block;
}
.dot {
  height: 8px;
  width: 8px;
  margin: 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
}

.dot-selected {
  height: 9px;
  width: 9px;
  margin: 2px;
  background-color: #000000;
  border-radius: 50%;
  display: inline-block;
}
</style>
