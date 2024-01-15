<template>
  <div>
    <the-header></the-header>
    <the-resource></the-resource>
  </div>
</template>

<script>
import TheHeader from './components/layouts/TheHeader.vue'
import TheResource from './components/resources/TheResource.vue'
export default {
  components: { TheHeader, TheResource },
  data() {
    return {
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>