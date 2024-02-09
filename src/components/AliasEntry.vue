<template>
  <div>
    <input 
    :value="item" 
    @input="(event) => handleAliasUpdate(event)"
    >
  </div>
</template>

<script>
export default {
  props: {
    item: String
  },
  methods: {
    handleAliasUpdate(event){
      
      this.$emit('change', event.target.value)
    }
  },
  mounted(){
    console.log(this.item)
  }
};
</script>