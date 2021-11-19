<template>
  <div>
    <h1>Minha lista de tarefas</h1>

    <button @click="handlerShowHideList">
      Ver a lista!
    </button>
    <br>
    <input 
      type="text" 
      @keyup.enter="addTask"
      v-focus 
      v-model="state.currentTask">

    <ul v-if="state.showList">
      <li
        v-for="(task, index) in state.tasks"
        @dblclick="complete(task)"
        :key="`${task}-${index}`"
        class="task-item"
        :class="{
          'line-through': task.isDone
        }"
      >
        {{task.name}}

        <button 
          @click="remove(task)"
        >&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tarefas escondida</p>
  </div>
</template>

<script>
import { reactive } from 'vue'

const focus = {
  inserted: (element) => { /* o inserted é uma propriedade da diretiva... */
    element.focus()
  }
}

export default {
  directives: {
    focus
  },
  setup() {
    const state = reactive({
      currentTask: '',
      showList: false,
      tasks: [
        {name: 'Fazer o curso', isDone: false}
      ]
    })

    function handlerShowHideList() {
      state.showList = !state.showList
    }

    function remove(task) {
      console.log('task', task)
      state.tasks = state.tasks.filter(t => t.name !== task.name)
    }

    function complete(task) {
      state.tasks = state.tasks.map(t => {
        if(t.name === task.name) {
          return {...t, isDone: !t.isDone}
        }
        return {...t}
      })
    }

    function addTask() {
      state.tasks.push({
        name: state.currentTask,
        isDone: false
      })

      state.currentTask = ''
    }

    return {
      state,
      handlerShowHideList,
      remove,
      complete,
      addTask
    }
  }
}
</script>

<style scoped> /* hash para escopar os elementos */
.line-through {
  text-decoration: line-through;
}
.task-item {
  cursor: pointer;
}
</style>