<template>
  <GuestBook/>
</template>


<style>
body {
  background-color: blueviolet;
  min-height: 100vh;
}
</style>


<script>
import GuestBook from './views/GuestBook.vue'

export default {
  name: 'App',
  components: {
    GuestBook
  }
}
</script>
