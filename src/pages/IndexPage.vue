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
      disableStats: true
    })

    window.Echo.channel('home').listen('NewMessage', (e) => {
      console.log(e.message)
    })
  }
})
</script>
