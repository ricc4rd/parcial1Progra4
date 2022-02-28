<template >
    <div class="container">
        <h2>To-Do App</h2>

        <!-- creamos el input -->
        <div class="d-flex">
            <input v-model="task" type="text" class="form-control" placeholder="Ingresa la tarea">
            <button @click="enviarTask" class="btn btn-warning rounded-0">Enviar</button>
        </div>

        <!-- HACEMOS LA TBLA DE TAREAS AYUDANDONOS CON BOOTSTRAP -->
        <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">Tareas pendientes</th>
      <th scope="col">Estado de las tareas</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>{{task.name}} </td>
      <td>
           <span class="pointer">{{task.status}}</span>
    </td>
      <td>
          <div class="text-center" @click="editarTask(index)">
              <span class="fa fa-pen"></span>
          </div>
      </td>
      <td>
          <div class="text-center" @click="borrarTask(index)">
              <span class="fa fa-trash"></span>
          </div>
      </td>
    </tr>
  </tbody>
</table>
    </div>
</template>

<script>
export default {
name: "HelloWorld",
props: {
    msg: String,
},

    data(){
        return{
            task: '',
            editedTask: null,
            estados: ['En proceso', 'Pendientes', 'Terminado'],
            tasks: [
                {
                    name: 'hacer ejercicio a las 6:00 am mañana',
                    status: 'Pendiente'
                },
                {
                    name: 'hacer el parcial de programación',
                    status: 'En proceso'
                }
            ]
        }
    },
    methods: {
       enviarTask(){
           if(this.task.length === 0) return 0;

        if(this.editedTask === null) { 
           this.tasks.push({
               name: this.task,
               status: 'Pendiente'
           });

           }else{
               this.tasks[this.editedTask].name = this.task;
               this.editedTask = null;

           }


           this.task = '';
       },
       borrarTask(index){
           this.tasks.splice(index,1);
       },

       editarTask(index){
          this.task = this.tasks[index].name;
          this.editedTask = index;
       },
       

    }
};
</script>


<style scoped>
.pointer{
    cursor: pointer;
}
</style>