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
  import axios from 'axios'
export default {
  data: function () {
    return {
      info : null,
      message: "Hello Vue!",
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' }
      ],
      message2: 'Hello Vue.js!'
    }

  },

  mounted () {
    axios.get('http://localhost:3000/todos', { headers: { 'Authorization': "eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoyLCJleHAiOjE1NjUxODE5NDV9.sgQI0l5qQnl-Bl7kKdSQs3ONt3xECO1xWbugfYjxqU0" } })
            .then(response => (this.info = response.data[0].id + " " + response.data[0].title + " " + response.data[0].created_at + " " + response.data[0].created_by))
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
