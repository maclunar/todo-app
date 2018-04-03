<template>
  <div class="hello">
    <h1>Tasks</h1>
    <ul v-for="task in tasks">
      <li>{{ task.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Tasks',
  data () {
    return {
      tasks: [
        { title: 'Learn Vue.js', completed: false },
        { title: 'Make coffee', completed: true }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
