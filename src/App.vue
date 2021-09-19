<template>
<div id="Todo">
  <form v-on:submit.prevent="addNewTask">
    <label for="new-Task">Add a task </label>
    <input
      v-model="newTaskText"
      id="new-task"
      placeholder="My new task"
    />
    <button>Add</button>
  </form>

  <ul>
    <li v-for="(task, index) in tasks"
      :key="task.id"
      :title="task.title">
        {{ task.title }}
      <button @click="removeTask(index, tasks)">Done</button>
    </li>
  </ul>
</div>
</template>

<script>
//import Tasks from './Components/Task'

export default {
   data() {
    return {
      newTaskText: '',
      tasks: [
        {
          id: 1,
          title: 'task 1'
        },
        {
          id: 2,
          title: 'task 2'
        },
        {
          id: 3,
          title: 'task 3'
        }
      ],
    }
  },
  methods: {
    addNewTask() {
      this.tasks.push({
        id: this.id++,
        title: this.newTaskText
      })
    },
    removeTask(int, object){
      object.splice(int, 1)
    }
  },
  props: ['title'],
  emits: ['remove'],
}
</script>

<style scoped>
.demo {
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  user-select: none;
  overflow-x: auto;
}
</style>
