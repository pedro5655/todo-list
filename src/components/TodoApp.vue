<template>
  <div class="body">
  
  <div class="container">
<h2 class="text-center mt-5">Lista de Afazeres</h2>


<!-- input -->

<div class="d-flex">
  <input  v-model="task"   type="text" placeholder="Nova Tarefa..." class="form-control" >
  <button  @click="submitTask" class="btn btn-warning rounded-0">Add</button>
</div>

<!-- Task table -->

<table class="table table-bordered mt-5" >
  <thead>
    <tr>
      <th scope="col">Tarefas</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index" >
      <td>
      <span :class="{'finished': task.status === 'Concluído'}">  {{ task.name }} </span>
        </td> 
      <td style="width: 120px"><span @click="changeStatus(index)" class="pointer"
      :class="{
                'text-danger': task.status === 'À fazer',
                'text-success': task.status === 'Concluído',
                'text-warning': task.status === 'Em andamento',
              }"
      
      
      
      >
        {{ task.status }}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen" ></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash" ></span>
        </div>
      </td>
    </tr>
  
  </tbody>
</table>


  </div>
  
  


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      
      task: '',
      editedTask: null,
      availableStatuses: ['Em andamento', 'À fazer', 'Concluído'],


      tasks: [
        {
          name: 'Estudar CODE 25h por dia',
          status: 'À fazer'
          
        },
        
        {
          name: 'Dormir menos de 4 horas por noite',
          status: 'À fazer'
          
        }
         
      ]
    }
  },        
   methods: {
     submitTask() {
       if(this.task.lenght === 0) return;
       
       if(this.editedTask === null){

       this.tasks.push({
         name: this.task,
         status: 'Lista'
       });
       } else{
         this.tasks[this.editedTask].name = this.task;
         this.editedTask = null;
       }
       this.task = '';
     },
       deleteTask(index){
         this.tasks.splice(index, 1)
       },

       editTask(index) {
       this.task = this.tasks[index].name;
       this.editedTask = index;
       },

       changeStatus(index){
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
       if(++newIndex > 2) newIndex = 0;
       this.tasks[index].status = this.availableStatuses[newIndex];
       },


   }

 
}
</script>


<style>
.pointer {
  cursor: pointer;
}

.finished {
  text-decoration: line-through;
}



body{
  background: rgb(96, 67, 100);
background: linear-gradient(90deg, rgb(139, 111, 143) 0%, rgb(159, 132, 190) 28%, rgb(161, 132, 160) 35%, rgb(149, 93, 114) 100%);

 
}

.container{
  
  margin-top: 10rem;
  box-shadow: 9px 4px 25px -7px rgba(128, 44, 118, 1);
  border-radius: 100px 42px 47px; 
  border: 2px solid #ebd9e8;
}



</style>
