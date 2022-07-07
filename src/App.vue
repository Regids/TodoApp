<template>
  <div class="Jumbotron bg-primary text-light">
    <div class="container">
      <b>
        <h1 class="display-4">Todo App</h1>
        <p class="lead">Manage day-to-day tasks with ease</p>
      </b>
    </div>
  </div>
  <br>
  <div class="container">
    <div class="row">
      <div class="offset-3 col-md-4">
        <input type="text" id="taskip" @keydown.enter="insertItem()" v-model="todoItem" placeholder="Add task here">
      </div>
    </div>
    <br>
    <div class="row">
      <div class="col-md-12">
        <h3>Task List</h3>
        <table class="table table-striped">
          <thead class="thead-dark">
              <th>ID</th>
              <th>Name</th>
              <th>Mark as completed</th>
              <th>Remove</th>
          </thead>

          <tbody>
            <tr v-for="(task,index) in todoList" v-bind:key="task">
              <td>{{task.id}}</td>
              <td>
                <div v-if="!task.editing" @dblclick="editTask(task)" v-bind:class="{completed: task.isCompleted}">{{task.name}}</div>
              <input @blur="editCompleted(task)" @keydown.enter="editCompleted(task)" v-model="task.name" v-else type="text">
              </td>
              <td><input v-model="task.isCompleted" type="checkbox"></td>  
              <td><button @click="removeItem(index)" class="btn btn-sm btn-danger">Remove</button></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return{
      todoItem:'',
      id:0,
      todoList:[],
    }
  },
  methods:{
    insertItem(){
      this.todoList.push({name:this.todoItem, isCompleted:false,id:this.id++,editing:false})
      this.todoItem=''
    },
    editTask(task){
      task.editing=true
    },
    editCompleted(task){
      task.editing=false
    },
    removeItem(index){
      this.todoList.splice(index,1)
    }
  }
}
</script>

  
<style>

  .completed{
    text-align: center;
    text-decoration: line-through;
    color:gray;
  }
  .Jumbotron {
    background-color: #015453 !important; /* Cambia color de todo app*/
    box-shadow:0 40px 20px 0 rgba(0, 0, 0, 0.2) ;
  }

  #taskip{
    border-radius: 3px;
    border-bottom: 2px solid lightgrey;
    height: 40px;
    position: absolute;
    text-align: center; 
    width: 300px;
    
    
  }
</style>
