<template>
  <q-page class="flex flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import Echo from 'laravel-echo'
window.Pusher = require('pusher-js')

export default defineComponent({
  name: 'IndexPage',
  mounted () {
    window.Echo = new Echo({
      broadcaster: 'pusher',
      key: 'ASDASD2121',
      wsHost: window.location.hostname,
      wsPort: 6001,
      forceTLS: false,
      disableStats: true
    })

    window.Echo.channel('home').listen('.NewMessage', (e) => {
      console.log(e)
    })
  },
  methods: {
    saludar: async function () {
      try {
        const data = await fetch('http://localhost:8000/api/saluda')
        const response = await data.json()
        console.log(response.saludo)
      } catch (error) {
        console.error(error)
      }
    }
  }
})
</script>
