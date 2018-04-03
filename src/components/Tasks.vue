<template>
  <div class="hello">
    <h1>Tasks</h1>

    <form @submit.prevent="addTask">
      <input type="text" placeholder="Enter a new task..." v-model="task.title">
      <input type="checkbox" id="completed" v-model="task.completed">
      <label for="completed">Completed?</label>
    </form>

    <ul v-for="task in tasks">
      <li>{{ tasks.indexOf(task) + 1 }}. {{ task.title }}</li>
      <button v-if="!task.completed">Complete</button>
    </ul>
    <p v-if="tasks.length < 1">No tasks to see here. Carry on.</p>
    <p>Tasks left to complete: {{ tasksNotCompleted() }}</p>
  </div>
</template>

<script>
export default {
  name: 'Tasks',
  data () {
    return {
      task: { title: '', completed: false },
      tasks: [
        { title: 'Learn Vue.js', completed: false },
        { title: 'Book concert tickets', completed: false },
        { title: 'Buy lime to make cuba libre', completed: false },
        { title: 'Make coffee', completed: true }
      ]
    }
  },
  methods: {
    tasksNotCompleted() {
      var notCompleted = 0;
      for (let task of this.tasks) {
        if (!task.completed) {
          notCompleted++;
        }
      }
      return notCompleted;
    },

    addTask() {
      this.tasks.push({ title: this.task.title, completed: this.task.completed });
      this.task = { title: '', completed: false };
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
