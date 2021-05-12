<template>
  <div class="composition">
    <h1>This is an Reactive Composition API page</h1>
    <h1>You Have {{todosCount}} todos</h1>
    <div>
      <input v-model="newTodoName" @keyup.enter="addtodo" placeholder="Add a Todo" type="text">
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{todo.name}}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { computed, ref, watch} from 'vue'

export default {
  name: 'Options',
  setup() {
    let newTodoName = ref('')
    let todos = ref([])
    const swearwords = ['fart', 'butt hair', 'willy']

    let todosCount = computed(() => {
      return todos.value.length
    })

    function addtodo() {
      // console.log('adfadsf')
      let newTodo = {
        id: Date.now(),
        name: newTodoName.value
      }
      todos.value.push(newTodo)
      newTodoName.value = ''
    }

    function deleteTodo(index) {
      todos.value.splice(index, 1)
    }

    watch(newTodoName, (newValue) => {
        console.log('newValue: ', newValue)
        if(swearwords.includes(newValue.toLowerCase())) {
          newTodoName.value = ''
          alert(' You must NEVER say ' + newValue + '!!')
        }
      })
    
    return {
      newTodoName, todos, todosCount, addtodo, deleteTodo
    }

  }
}
</script>
<style>
ul{
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}
li{
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}
li span{
  flex-grow: 1;
}

</style>
