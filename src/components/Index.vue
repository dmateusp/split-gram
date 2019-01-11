<template>
  <div>
    <h1> Test </h1>
    <ImageActions/>
  </div>
</template>

<script>
import ImageActions from '@/components/ImageActions'

export default {
  name: 'Index',
  components: {
    'ImageActions': ImageActions
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
</style>
