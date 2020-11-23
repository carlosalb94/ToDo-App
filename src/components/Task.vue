<template>
  <div>
    <div class="card w-75  h-75 mx-auto my-2 shadow rounded" >
      <div class="card-body" :style="cssCardColor">
        <p class="text-justify">{{ texto }}</p>
      </div>
      <div :style="cssCardColor" class="card-footer d-flex justify-content-around px-md-0  px-sm-0 px-lg-0">
        <button  class="btn btn-md btn-secondary p-2 d-flex" type="button" v-on:click="deleteEvent"><i class="material-icons">delete</i></button>
        <button  v-show="!this.finished" class="btn btn-secondary mx-1" type="button" v-on:click="finishTask">Finalizada</button>
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
        chekedIconSize: 2.1,
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
            'font-size': this.chekedIconSize+"em",
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
