<template>
  <div class="Options">
    <img alt="Vue logo" src="../assets/logo.png">    
    <h1>This is an Options API page</h1>
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

export default {
  name: 'Options',
  data(){
    return {
      newTodoName: '',
      todos: [
        {
          id: 1,
          name: 'one'
        },
        {
          id: 2,
          name: 'Two'
        },
        {
          id: 3,
          name: 'Three'
        }
      ],
      swearwords: ['fart', 'butt hair', 'willy']
    }
  },
  computed: {
    todosCount() {
      return this.todos.length
    }
  },
  methods: {
    addtodo() {
      // console.log('adfadsf')
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName
      }
      this.todos.push(newTodo)
      this.newTodoName = ''
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
    }
  },
  watch: {
    newTodoName(newValue) {
      console.log('newValue: ', newValue)
      if(this.swearwords.includes(newValue.toLowerCase())) {
        this.newTodoName = ''
        alert(' You must NEVER say ' + newValue + '!!')
      }
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
