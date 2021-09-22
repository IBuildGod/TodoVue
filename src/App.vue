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
      :priority="task.priority"
      :color="task.color"
      class="text-white list-disc break-words pl-2 my-1 w-full"
      :style="{background: task.color}"
      >
        {{ task.title }}
        <div class="relative inline-block float-right">
            <select @change="onChange($event, index)" class=" text-white border-2 border-gray-300 rounded z-1 bg-gray-500 mr-2">
              <option disabled selected value>Set Priority</option>
              <option v-for="item in importance" :key="item.id" :value="item.rating">
                {{ item.rating }}
              </option>
            </select>
          </div>
      <button @click="removeTask(index, tasks, task.id, task.title, task.priority, task.color)" class="float-right hover:bg-gray-300 mr-3 rounded px-2 place-items-center hover:text-black">x</button>
    </li>
  </ul>
</div>
</template>

<script>
//import Tasks from './Components/Task'

export default {
   data() {
    return {
      newColor: '',
      newTaskText: '',
      tasks: [
        {
          id: 1,
          title: 'task 1',
          priority: 0,
          color: '#424242',
        },
        {
          id: 2,
          title: 'task 2',
          priority: 0,
          color: '#424242',
        },
        {
          id: 3,
          title: 'task 3',
          priority: 0,
          color: '#424242',
        }
      ],
      newtaskId: 4,
      deletedtasks: [{}],
      importance: [
        {
          id: 1,
          rating: 0,
          backgroundColor: '#424242',
        },
        {
          id: 2,
          rating: 1,
          backgroundColor: 'red',
        },
        {
          id: 3,
          rating: 2,
          backgroundColor: 'orange',
        },
        {
          id: 4,
          rating: 3,
          backgroundColor: '#8B8000',
        },
        {
          id: 5,
          rating: 4,
          backgroundColor: 'green',
        },
        {
          id: 6,
          rating: 5,
          backgroundColor: 'blue',
        },
      ],
      dropdownItems: [{
        text:'Set priority',
        index: 1
      }, 
      ],
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
        color: '#424242',
      })
    },
    removeTask(taskIndex, listName, id, title, priority, color){
      listName.splice(taskIndex, 1)
      this.deletedtasks.push({
        title: title,
        id: id,
        priority: priority,
        color: color,
      }),
      console.log(this.deletedtasks)
    },
    onChange(event, index) {
      this.tasks[index].color = this.importance[event.target.value - 1].backgroundColor
      this.tasks[index].priority = event.target.value
      console.log(this.importance[event.target.value - 1].backgroundColor)
    },
  },
}
</script>