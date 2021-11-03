<template>
  <v-main />
</template>

<script>
import vMain from '../components/v-main.vue'
export default {
  components: { vMain }
}
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html {
  font-family: "Open Sans";
  font-style: normal;
  font-weight: normal;
}

body{
   background: #f2f2f2;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
