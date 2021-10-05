<template>
  <div class="home">
    <h1>TurnTable</h1>
    <turntableCahrt />
  </div>
</template>

<script>
// @ is an alias to /src
import turntableCahrt from '../components/turntableCahrt.vue'

export default {
  name: "Home",
  components:{
    turntableCahrt,
  }
};
</script>
<style scoped>
.home {
  margin-top: 20px;
}
</style>
