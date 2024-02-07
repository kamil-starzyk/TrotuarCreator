<template>
  <div class="editor_panel">
    <h1 @click="togglePanel">Player Details</h1>
    <div v-show="panelVisible">
      <p>mob ID: <input
        :value="player.mob_id" 
        @input=" ( event ) => handleUpdate(event, 'mob_id', true)"
        type="number"
      ></p>
      <p>Coordinates: 
        x: <input 
        :value="player.x" 
        @input=" ( event ) => handleUpdate(event, 'x', true)"
        type="number" style="width: 30px"
        >
        y: <input 
        :value="player.y" 
        @input=" ( event ) => handleUpdate(event, 'y', true)"
        type="number" style="width: 30px"
        >
        z: <input 
        :value="player.z" 
        @input=" ( event ) => handleUpdate(event, 'z', true)"
        type="number" style="width: 30px"
        >
      </p>
      <p>Base Name: <input
        :value="player.base_name" 
        @input=" ( event ) => handleUpdate(event, 'base_name')"
      ></p>
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
      <p>attack: <input
        :value="player.stats.attack" 
        @input=" ( event ) => handleUpdate(event, 'stats.attack', true)"
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