<template>
  <div :style="setCustomBoardColor">
    <div class="input-group col-lg-6 col-md-6 col-sm-6  mx-auto">
      <input
        class="input-group-text bg-light col-lg-12 mx-auto col-md-12 col-sm-12"
        v-model="textoInput"
        v-on:keyup.enter="newTask(textoInput)" 
        type="text"
        placeholder="Agregar tarea"
      />
      <button class="btn btn-secondary col-lg-6 col-md-6 mx-auto mt-3" type="button" v-on:click="deleteAllTasks">Borrar finalizadas</button>
    </div>
    <div class="row-lg row-sm row-md d-flex justify-content-center mt-3">
      <div class="col-lg-6 col-md-6 col-sm-6 border-right">
        <h5 class="text-center mb-4">Pendientes</h5>
          <Task
            v-show="!tarea.finished"
            v-for="tarea in tareas"
            v-bind:key="tarea.id"
            v-bind:texto="tarea.texto"
            v-bind:finished="tarea.finished"
            v-bind:id="tarea.id"
            v-on:delete-task="deleteTask(tarea.id)"
            v-on:finish-task="finishTask(tarea.id)"
          />
      </div>
      <div class="col-lg-6 col-md-6 col-sm-6 border-left">
        <h5 class="text-center mb-4">Finalizadas</h5>
        <Task
          v-show="tarea.finished"
          v-for="tarea in tareas"
          v-bind:key="tarea.id"
          v-bind:texto="tarea.texto"
          v-bind:finished="tarea.finished"
          v-bind:id="tarea.id"
          v-on:delete-task="deleteTask(tarea.id)"
          v-on:finish-task="finishTask(tarea.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Task from "@/components/Task";


export default {
  name: "Board",
  components: { Task },

  data() {
    return {
      boardColor:"#e0ece4",
      textoInput: "",
      tareas: [],
      idCount: 0,
    };
  },

  computed:{
    setCustomBoardColor() {
      return {
       'background-color':this.boardColor
      }
    }
  },

  methods: {

    deleteAllTasks() {
      const newTask = []
      this.tareas.forEach(function(element){
        if (!element.finished) {
          newTask.push(element)
        }
      })
      this.tareas = newTask
      this.idCount = 0
    },

    deleteTask(id) {
      const indexId = this.tareas.findIndex((task => id === task.id))
      if (indexId >=0 ) {
        if (this.tareas[indexId].finished)
          this.tareas.splice(indexId, 1)
        else if(confirm('Esta tarea aun no ha finalizado. ¿Desea borrar de todas maneras?'))
          this.tareas.splice(indexId, 1)
      }
    },

    newTask(text){
      if (text) {
        const task = {
          id:this.idCount,
          texto:text,
          finished: false,
        }
        this.idCount++
        this.tareas.push(task)
        this.textoInput = ""
      } 
    },

    finishTask(id) {
      const indexId = this.tareas.findIndex((task => id === task.id))
      if (indexId >= 0) {
        this.tareas[indexId].finished = !this.tareas[indexId].finished;
      }
    }
  }
};
</script>

<style scoped>
  
</style>