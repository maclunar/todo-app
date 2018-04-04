<template>
  <div class="hello">
    <h1>Tasks</h1>

    <form @submit.prevent="addTask">

      <input type="text" placeholder="Enter a new task..."
        v-model="task.title" v-validate="'required|min:5'" name="title"
      >

      <input type="checkbox" id="completed" v-model="task.completed">
      <label for="completed">Completed?</label>

      <button>Add new task</button>

      <p class="alert" v-if="errors.has('title')">{{ errors.first('title') }}</p>
    </form>

    <ul v-for="task in tasks">
      <i class="fa fa-circle" v-if="!task.completed" v-on:click="completeTask(task)"></i>
      <i class="fa fa-check-circle" v-else v-on:click="uncompleteTask(task)"></i>
      <li v-bind:class="{ completed: task.completed }">
        {{ task.title }}
      </li>
      <i class="fa fa-times-circle" v-on:click="removeTask(task)"></i>
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

    completeTask(task) {
      task.completed = true;
    },

    uncompleteTask(task) {
      task.completed = false;
    },

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
      this.$validator.validateAll().then((result) => {
        if (result) {
          this.tasks.push({ title: this.task.title, completed: this.task.completed });
          this.task = { title: '', completed: false };
        } else {
          console.log('task in not valid');
        }
      })
    },

    removeTask(task) {
      this.tasks.splice(this.tasks.indexOf(task), 1);
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
.completed {
  color: #888;
  text-decoration: line-through;
}
a {
  color: #42b983;
}
label {
  font-size: 14px;
}
.alert {
  font-weight: bold;
  font-size: 12px;
  color: #777;
}
</style>
