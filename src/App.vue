<template>

<div class="app-wrapper">
     <div id="app">
  
    <h3>Todo</h3> 
    <form v-on:submit.prevent="addNewTodo">
            <input type="text"   v-model="newTodoText">
            
         <button>Add</button>
    </form>
  <TodoItem 
        @todo-deleted="deleteTodo"
        :key="item.id" 
        v-for="item in taskList" 
        :todo="item">
        
    </TodoItem>
    
   
  </div>
</div>
 
</template>

<script>
import TodoItem from './components/TodoItem.vue';

export default {
  name: 'App',
  data() {
    return {
        newTodoText: '',
      taskList: [
        {
          id: 1,
          task: "Wash cloths",
          state: "pending"
        },
        {
          id: 2,
          task: "Submit assignment",
          state: "pending"
        },
        {
          id: 3,
          task: "Write user story",
          state: "done"
        },
        {
          id: 4,
          task: "Read book",
          state: "pending"
        }
      ],
          nextTodoId: 5
    }
  },
 
  components: {
    TodoItem // Local registration
  },
  methods: {
    addNewTodo() {
      this.taskList.push({
        id: this.nextTodoId++,
        task: this.newTodoText,
        state:'pending'
      })
      this.newTodoText = ''
    },
  
    deleteTodo(id) {
      
      let newTaskList = [];
      let item;
      for (item of this.taskList) {
        if(item.id != id) {
          newTaskList.push(item)
        }
      }
      this.taskList = newTaskList;
    },
    addIsCalled() {
      console.log('added');
    },
    deleteIsCalled() {
      console.log('deleted');
    },
    pendingIsCalled() {
      console.log("pending");
    },
    doneIsCalled() {
      console.log("done");
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  
}
.app-wrapper{
  display: flex;
  justify-content: center;
}
input{
  width: 350px;
    height: 25px;
    margin-bottom: 20px;
}
button{
  background: blue;
  width: 50px;
  color: white;
  height: 30px;
  border-style: none;
  margin-left:20px ;
}
</style>
