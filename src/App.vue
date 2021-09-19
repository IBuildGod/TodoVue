<template>
<div id="Todo" class="bg-gray-800 border-2 border-gray-50 p-3 max-w-lg">
  <form v-on:submit.prevent="addNewTask" class="mb-5">
    <label for="new-Task" class="pr-2 text-2xl text-white">Add a task </label>
    <input
      v-model="newTaskText"
      id="new-task"
      placeholder="My new task"
      class="border-2 border-gray-50 rounded p-1 placeholder-gray-400 bg-gray-800 font-medium text-white"
    />
    <button class="ml-2 px-2 py-1 border-2 border-gray-50 text-white rounded hover:bg-gray-300 hover:text-black">Add</button>
  </form>

  <ul class="border-2 border-gray-50 ml-5 flow-root">
    <li v-for="(task, index) in tasks"
      :key="task.id"
      :title="task.title"
      class="text-white pl-2 list-disc my-1 break-words w-full">
        {{ task.title }}
      <button @click="removeTask(index, tasks)" class="float-right mr-3 hover:bg-gray-300 rounded px-2 place-items-center hover:text-black">x</button>
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
      newtaskId: 4,
    }
  },
  methods: {
    addNewTask() {
      console.log(this.newtaskId)
      if(this.newTaskText)
      this.tasks.push({
        id: this.newtaskId++,
        title: this.newTaskText,
        newTaskText: "",
      })
    },
    removeTask(taskIndex, listName){
      listName.splice(taskIndex, 1)
    }
  },
  props: ['title'],
  emits: ['remove'],
}
</script>
