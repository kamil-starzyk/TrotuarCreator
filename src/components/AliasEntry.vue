<template>
  <div>
    <input 
    :value="item" 
    @input="(event) => handleAliasUpdate(event)"
    >
  </div>
</template>

<script>
import { toRaw } from 'vue'
export default {
  props: {
    item: String
  },
  methods: {
    handleAliasUpdate(event){
      const record = structuredClone(toRaw(event.target.value))
      console.log("benc " + record)
      this.$emit('change', record)
      console.log(event.target.value)
    }
  },
  mounted(){
    console.log(this.item)
  }
};
</script>