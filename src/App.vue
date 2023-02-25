<template>
    <header>
      <Search  v-on:query-change="querySearch"/>
    </header>
    <div id="mainContainer">
      <h2>To Do: Lists & Tasks</h2>
      <ToDoAdd v-on:add-todo="addTodo" />
      <ToDos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo" />
    </div>
</template>


<script>
  import Search from './components/Search.vue';
  import ToDos from './components/ToDos.vue'
  import ToDoAdd from './components/ToDoAdd.vue';

  export default {
    name: 'App',
    components: {Search, ToDos, ToDoAdd},
    methods: {
      deleteTodo (id) {
        this.todos =  this.todos.filter(todo => todo.id !== id)
        this.copyTodos = [... this.todos]
      },
      addTodo(todo){
        this.todos.push(todo)
        this.copyTodos = [... this.todos]
      },
      querySearch(query){
        if(query.trim() === ''){
          this.copyTodos = [... this.todos]
        }else{
          const temp = this.todos.filter(todo => {
            return todo.title.toLowerCase().includes(query)
          });
          this.copyTodos = [... temp]
        }
      }
    },
    data(){
      return{
        todos: [
          {
            id: 0,
            title: 'Comprar la cena',
            completed: false
          },
          {
            id: 1,
            title: 'Sacar a pasear al perro',
            completed: true
          },
          {
            id: 2,
            title: 'Ver Netflix',
            completed: false
          },
        ],
        copyTodos: []
      }
    },
    created(){
      // duplicamos el arregalo de todos
      this.copyTodos = [...this.todos]
    }
  } 

</script>

<style>

*{
  box-sizing: border-box;
}

html, body {
  height: 100%;
  width: 100%;
}

body {
font-family: Arial, Helvetica, sans-serif;
font-size: 1.5em;
padding: 0;
margin: 0;
background: linear-gradient(#2c3e50, #3498db);
}

#mainContainer{
  border: solid 1px #ccc;
  width: 600px;
  margin: 100px auto;
  background: white;
  border: 1px solid black;
  box-shadow: 5px 2px 20px;
}

header {
  background: black;
  padding: 10px;
  width: 100%;
}

h2{
  padding: 0 10px;
}

@media only screen and (min-width: 355px) {
  #mainContainer{
  width: 350px;
  }
  h2{
  font-size: inherit;
  padding: 0 10px;
}
}

</style>