<template>
  <div class="hero is-fullheight">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-centered">

          <div class="column is-4">
            <p class="title white">GuestBook</p>
            <p class="subtitle white">Deixe sua mensagem!</p>

            <form @submit.prevent="send_data" class="box">
              <div class="field">
                <label class="label">Seu nome</label>
                <div class="control">
                  <input class="input" type="text" name="name" v-model="form.author">
                </div>
              </div>
              <div class="field">
                <label class="label">Sua mensagem</label>
                <div class="control">
                  <textarea class="textarea" name="message" v-model="form.text"></textarea>
                </div>
              </div>
              <div class="field">
                <button type="submit" class="button is-success">Enviar</button>
              </div>
            </form>

          </div>

          <div class="column is-8">
            <div v-for="message in messages" :key="message.id">
              <div class="box">
                <div class="content">
                  <p class="subtitle">{{ message.author }}</p>
                  {{ message.text }}
                </div>
              </div>
              <br>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.white {
  color: whitesmoke;
}
.hero {
  background-color: blueviolet;
}
</style>


<script>
import axios from "axios"

export default {
  name: 'GuestBook',

  data() {
    return {
      messages: [],
      form: {
        author: null,
        text: null,
      }
    }
  },

  created() {
    const api_url = `${process.env.VUE_APP_API_URL}/messages`
    axios.get(api_url).then((response) => {
      this.messages = response.data
    })
  },

  methods: {
    send_data() {
      const api_url = `${process.env.VUE_APP_API_URL}/messages/`
      const payload = {
        author: this.form.author,
        text: this.form.text,
      }
      axios.post(api_url, payload).finally(() => {
        this.form.author = null
        this.form.text = null
      })
    }
  }
}
</script>
