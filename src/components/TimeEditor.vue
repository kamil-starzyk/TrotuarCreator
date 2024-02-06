<template>
  <div>
    <h1>Time Details</h1>
    <div>
      <p>Seconds: <input
        :value="time.s" 
        @input=" ( event ) => handleUpdate(event, 's')"
      ></p>
      <p>Minutes: <input
        :value="time.m" 
        @input=" ( event ) => handleUpdate(event, 'm')"
      ></p>
      <p>Hours: <input
        :value="time.h" 
        @input=" ( event ) => handleUpdate(event, 'h')"
      ></p>
      <p>Days: <input
        :value="time.d" 
        @input=" ( event ) => handleUpdate(event, 'd')"
      ></p>
      <p>Week Day: <input
        :value="time.week_d" 
        @input=" ( event ) => handleUpdate(event, 'week_d')"
      ></p>
      <p>Week: <input
        :value="time.w" 
        @input=" ( event ) => handleUpdate(event, 'w')"
      ></p>
      <p>Season: <input
        :value="time.sn" 
        @input=" ( event ) => handleUpdate(event, 'sn')"
      ></p>
      <p>Years: <input
        :value="time.y" 
        @input=" ( event ) => handleUpdate(event, 'y')"
      ></p>

    </div>
  </div>
</template>

<script>
export default {
  props: {
    time: Object // Define time as a prop
  },
  methods: {
    handleUpdate(event, key){
      const objekt = { ...this.time, [key]:event.target.value }
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
