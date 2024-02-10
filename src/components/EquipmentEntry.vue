<template>
  <input 
    :value="item.name" 
    @input="(event) => handleItemUpdate(event, 'name')"
  >
  <textarea
    :value="item.description" 
    @input="(event) => handleItemUpdate(event, 'description')"
  ></textarea>
  <input 
    :value="item.weight" 
    @input="(event) => handleItemUpdate(event, 'weight', true)"
    class="numeric_input"
  >
</template>

<script>
import { toRaw } from 'vue'
import _ from "lodash"
export default {
  props: {
    item: Object
  },
  methods: {
    handleItemUpdate(event, key, isNumber=false){
      const record = structuredClone(toRaw(this.item))
      const value = isNumber ? +event.target.value : event.target.value
      _.set(record, key, value)
    
      this.$emit('change', record)
    }
  },
  mounted(){
    console.log(this.item)
  }
};
</script>