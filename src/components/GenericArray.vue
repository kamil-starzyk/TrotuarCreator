<template>
  <span v-for="(item, index) in items" :key="index">
    <div>
      <template v-if="renderComponent">
        <component 
          :is="renderComponent" 
          :item="item" 
          @change="(value) => handleUpdate({ target:{value} }, index)"
        />
      </template>
  </div>
    <button @click="removeItem(index)">-</button>
  </span>
  <button @click="addItem">+</button>
</template>

<script>
import _ from "lodash"
import { toRaw } from 'vue'
export default {
  props: {
    items: Array,
    newItem: [Object, String],
    renderComponent: {type:Object}
  },
  methods: {
    handleUpdate(event, key, isNumber=false){
      const record = structuredClone(toRaw(this.items))
      const value = isNumber ? +event.target.value : event.target.value
      _.set(record, key, value)
    
      this.$emit('change', record)
      //console.log(objekt)
      console.log(this.items)
    },
    addItem() {
      const nextItems = structuredClone(toRaw(this.items));
      nextItems.push(structuredClone(toRaw(this.newItem)));
      this.$emit('change', nextItems)
    },
    removeItem(index) {
      const nextItems = structuredClone(toRaw(this.items))
      nextItems.splice(index, 1);
      this.$emit('change', nextItems)
    }
  },
  mounted(){
    console.log(this.items)
  }
};
</script>