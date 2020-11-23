<template>
  <div>
    <div class="card w-75  h-75 mx-auto my-2 shadow rounded" >
      <div class="card-body" :style="cssCardColor">
        <p class="text-justify">{{ texto }}</p>
      </div>
      <div :style="cssCardColor" class="card-footer d-flex flex-wrap justify-content-around px-md-1  px-sm-1 px-lg-1">
        <button  class="btn btn-lg btn-sm btn-secondary py-auto mb-1" type="button" v-on:click="deleteTask"><i class="material-icons">delete</i></button>
        <button  v-show="!this.finished" class="btn  btn-lg btn-sm btn-outline-success mb-1 mx-1" type="button" v-on:click="finishTask">Finalizar</button>
        <i v-show="this.finished" class="material-icons my-auto" :style="setFinishedCssProps">done</i>
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
      cssCardColor() {
        return {
          'background-color': this.cardColor,
        }
      },

      setFinishedCssProps() {
          return {
            'color': this.isFinishedColor,
            'font-size': this.chekedIconSize+"em",
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

      deleteTask () { return this.$emit('delete-task')},

    }
};
</script>
