<template>
  <div>
    <div class="content">
      <h1> split-gram </h1>
      <p>split your Instagram panoramas</p>
      <ImageSplittingApp/>
    </div>
    <div id="ui-footer">
      <footer class="footer">
        <div class="left bottom-column">Use Chrome or Firefox for compatibility</div>
        <div class="left bottom-column">
          <a href="https://github.com/dmateusp/split-gram"><img src="static/images/GitHub-Mark-64px.png" width="32px"/></a>
          <br/>
          v{{version}}
        </div>
        <div class="right bottom-column">
          split-gram does <b>not</b> download your images, everything happens in your browser
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
import ImageSplittingApp from '@/components/ImageSplittingApp'

export default {
  name: 'Index',
  components: {
    'ImageSplittingApp': ImageSplittingApp
  },
  data: function () {
    return {
      version: null
    }
  },
  mounted () {
    this.version = process.env.VERSION
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
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
footer {
  background-color: cornflowerblue;
  color: black;
  position: absolute;
  left: 0;
  bottom: 0;
  height: 90px;
  width: 100%;
  overflow: hidden;
  font-size: 13px;
}
.left {
  float: left;
}
.right {
  float: right;
}
.bottom-column {
  text-align: center;
  width: 33.33%;
  position: relative;
  top: 50%;
  transform: translateY(-50%);
  float: left;
}
</style>
<style>
html {
    position: relative;
    min-height: 100%;
}
body {
    margin: 0 0 100px;
    /* bottom = footer height */
    padding: 25px;
}
</style>
