<template>
  <div class="container">
    <appHeader></appHeader>
    <appMain></appMain>
  </div>
</template>

<script>
import appHeader from './components/appHeader.vue'
import appMain from './components/appMain.vue'

export default {

  components:{
    appHeader,
    appMain
  }
}
</script>

<style lang="scss" scoped></style>