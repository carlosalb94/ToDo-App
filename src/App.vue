<template>
  <div :style="setCustomBoardColor">
    <Board class="container-lg container-md container-sm py-5 px-3"/>
  </div>
</template>

<script>
import Board from "@/components/Board";

export default {
  name: "App",
  components: { Board },

  data() {
    return{
      boardColor:'#e0ece4',
      heightBoard:100
    }
  },

  computed:{
    setCustomBoardColor() {
      return {
       'background-color':this.boardColor,
       'min-height': this.heightBoard+"vh"
      }
    }
  },
};
</script>

<style>

</style>
