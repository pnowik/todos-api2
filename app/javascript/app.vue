<template>
  <div id="app">
    <p>{{ message }}</p>
    <ol>
      <li v-for="todo in todos">
        {{ todo.text }}
      </li>
    </ol>

    <p>{{ message2 }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>

    <p>{{ info }}</p>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      info: null,
      message: "Hello Vue!",
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' }
      ],
      message2: 'Hello Vue.js!'
    }

  },
  beforeMount () {
    axios
            .get('https://api.coindesk.com/v1/bpi/currentprice.json')
            .then(response => (this.info = response))
  },

  methods: {
    reverseMessage: function () {
      this.message2 = this.message2.split('').reverse().join('')
    }
  }

}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
