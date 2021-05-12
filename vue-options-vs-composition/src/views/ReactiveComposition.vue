<template>
  <div class="composition">
    <h1>This is an <strong>Reactive Data</strong> in Composition API page</h1>
    <h1>You Have {{todosCount}} todos</h1>
    <div>
      <input v-model="data.newTodoName" @keyup.enter="addtodo" placeholder="Add a Todo" type="text">
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in data.todos" :key="todo.id">
          <span>{{todo.name}}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { computed, reactive, watch} from 'vue'

export default {
  name: 'Options',
  setup() {
    
    let data = reactive({
      newTodoName: '',
      todos: []
    });

    const swearwords = ['fart', 'butt hair', 'willy']

    let todosCount = computed(() => {
      return data.todos.length
    })

    function addtodo() {
      // console.log('adfadsf')
      let newTodo = {
        id: Date.now(),
        name: data.newTodoName
      }
      data.todos.push(newTodo)
      data.newTodoName = ''
    }

    function deleteTodo(index) {
      data.todos.splice(index, 1)
    }

    watch(data, (newValue) => {
        console.log('newValue: ', newValue.newTodoName)
        if(swearwords.includes(newValue.newTodoName.toLowerCase())) {
          alert(' You must NEVER say ' + newValue.newTodoName + '!!')
          data.newTodoName = ''
        }
      })
    
    return {
      data, todosCount, addtodo, deleteTodo
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
