<template>
  <div id="app">
    <div v-if="check">
      If you see this, you are ready to continue.<br/>

      Delete the contents of the div#app element and continue with the project.
    </div>
    <div v-else>
      Something did not work as expected, troubleshoot time ...
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      check: false,
    }
  },
  mounted() {
    axios.get('http://localhost:3000/')
      .then(() => {
        this.check = true
      })
      .catch(error => {
        console.log(error)
      })
  },
}
</script>
