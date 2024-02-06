<template>
  <div class="editorPanel">
    <h1 @click="togglePanel">Time Details</h1>
    <div v-show="panelVisible">
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
  data() {
    return {
      panelVisible: false
    };
  },
  props: {
    time: Object // Define time as a prop
  },
  methods: {
    handleUpdate(event, key){
      const record = { ...this.time, [key]:event.target.value }
      this.$emit('change', record)
      //console.log(objekt)
      console.log(this.time)
    },
    togglePanel() {
      this.panelVisible = !this.panelVisible;
    }
  },
  mounted(){
    console.log(this.time)
  }
};
</script>
