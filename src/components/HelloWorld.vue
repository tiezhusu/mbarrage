<template>
  <div class="hello">
    <mbarrage></mbarrage>
  </div>
</template>

<script>
import mbarrage from '../lib/mbarrage/lib/mbarrage'
export default {
  name: 'HelloWorld',
  components:{
    mbarrage
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  position: relative;
  width: 1000px;
  height: 500px;
  margin: 0 auto;
}
</style>
