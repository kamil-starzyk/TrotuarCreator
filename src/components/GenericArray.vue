<template>

  <div class="root_div">
    <span v-for="(item, index) in items" :key="index" class="array_item">
      <template v-if="renderComponent">
        <component 
        :is="renderComponent" 
        :item="item" 
        @change="(value) => handleUpdate({ target:{value} }, index)"
        />
      </template>
      <button @click="() => removeItem(index)">-</button>
    </span>
    <div>
      <button @click="addItem">add item +</button>
    </div>
  </div>
  <div style="display: none" class="div_to_save_app_from_unexpected_crash"></div>
</template>

<style>
  .root_div{
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  .array_item{
    display:flex;
    align-items: center;
    gap: 8px;
  }
</style>
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
      if (event.target.value instanceof Event ) return //dis fix dirty as hell but what i gonna do

      const record = structuredClone(toRaw(this.items))
      const value = isNumber ? +event.target.value : event.target.value
      _.set(record, key, value)
      
      console.log("event: ", event)
      this.$emit('change', record)
      
      
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