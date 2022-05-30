<template>
  <div class="container">

    <div class="content">
      <h1>GuestBook</h1>
      <h5>Deixe sua mensagem!</h5>
    </div>

    <div v-for="message in messages" :key="message.id" class="box">
      <div class="content">
        <h3>{{ message.author }}</h3>
        <p>{{ message.text }}</p>
      </div>
    </div>

  </div>
</template>


<style scoped>
h1 {
  color: whitesmoke;
}
h5 {
  color: whitesmoke;
}
</style>


<script>
import axios from "axios"

export default {
  name: 'GuestBook',

  data() {
    return {
      messages: []
    }
  },

  created() {
    const api_url = `${process.env.VUE_APP_API_URL}/messages`
    axios.get(api_url).then((response) => {
      console.log(response);
      this.messages = response.data
    })
  },
}
</script>
