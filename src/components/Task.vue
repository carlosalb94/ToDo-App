<template>
  <div>
    <div class="card w-75 mx-auto my-2" >
      <div class="card-body" :style="cssCardColor">
        <p class="text-justify">{{ texto }}</p>
      </div>
      <div :style="cssCardColor" class="card-footer d-flex justify-content-around">
        <button  class="btn btn-secondary p-2 d-flex" type="button" v-on:click="deleteEvent"><i class="material-icons">delete</i></button>
        <button  v-show="!this.finished" class="btn btn-secondary" type="button" v-on:click="finishTask">Marcar como finalizada</button>
        <button  v-show="this.finished" class="btn btn-secondary" type="button" v-on:click="finishTask">Marcar como pendiente</button>
        <i v-show="this.finished" class="material-icons" :style="cssProp">done</i>
      </div>
    </div>
  </div>
</template>

<script>

export default {
    name: "Task",
    data () {
      return {
        chekedIconSize: 36,
        isFinishedColor: "#28df99",
        cardColor:"#f9f7cf",
      }
    },

    computed: {
      cssCardColor(){
        return {
          'background-color': this.cardColor,
        }
      },
      cssProp() {
        if (this.finished){
          return {
            'color': this.isFinishedColor,
            'font-size': this.chekedIconSize+"px",
          }
        } else {
          return {}
        }
      },
    },

    props: {
      id: Number,
      texto: String,
      finished: Boolean,
    },

    methods: {


      deleteAll () {return this.$emit('delete-all')},

      finishTask () {return this.$emit('finish-task')},

      deleteEvent() { return this.$emit('delete-task')},

    }
};
</script>
