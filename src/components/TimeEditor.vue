<template>
  <div>
    <h1>Time Details</h1>
    <div>
      <p>Seconds: {{ time.s }}</p>
      <p>Minutes: {{ time.m }}</p>
      <p>Hours: {{ time.h }}</p>

      <p>Hours: <input
        :value="time.h" 
        @input="handleUpdate"></p>
        <!-- Display other time properties -->

    </div>
  </div>
</template>

<script>
export default {
  props: {
    time: Object // Define time as a prop
  },
  methods: {
    handleUpdate(event){
      const objekt = { ...this.time, h:event.target.value }
      this.$emit('change', objekt)
      //console.log(objekt)
      console.log(this.time)
    }
  },
  mounted(){
    console.log(this.time)
  }
};
</script>
