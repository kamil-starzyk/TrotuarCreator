<template>
  <div class="editorPanel">
    <h1 @click="togglePanel">Player Details</h1>
    <div v-show="panelVisible">
      <p>Name: <input
        :value="player.name" 
        @input=" ( event ) => handleUpdate(event, 'name')"
      ></p>
      <h3>Stats</h3>
      <p>strength: <input
        :value="player.stats.strength" 
        @input=" ( event ) => handleUpdate(event, 'stats.strength', true)"
        type="number"
      ></p>

      <br>
    </div>
  </div>
</template>

<script>
import _ from "lodash"
export default {
  data() {
    return {
      panelVisible: false
    };
  },
  props: {
    player: Object // Define time as a prop
  },
  methods: {
    handleUpdate(event, key, isNumber=false){
      const record = structuredClone(this.player)
      const value = isNumber ? +event.target.value : event.target.value
      _.set(record, key, value)
    
      this.$emit('change', record)
      //console.log(objekt)
      console.log(this.player)
    },
    togglePanel() {
      this.panelVisible = !this.panelVisible;
    }
  },
  mounted(){
    console.log(this.player)
  }
};
</script>
