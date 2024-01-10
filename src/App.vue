<template>
  <div id="app">
    <div v-if="time">
      <TimeEditor :time="time" @change="(time) => Object.assign(this.time, time)"/>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
    <!-- Other components using specific data -->
  </div>
</template>

<script>
import TimeEditor from './components/TimeEditor.vue'; // Import the TimeDisplay component

export default {
  components: {
    TimeEditor // Register the TimeDisplay component
  },
  data() {
    return {
      gameData: {}, // Initialize data object to store time data
      time: {}
    };
  },
  created() {
    // Load demo.json and fetch necessary data
    fetch('data/demo.json') // Adjust the path as needed
      .then(response => response.json())
      .then(data => {
        this.gameData = data; // Store the entire data object from demo.json
        // this.time = data.time;
        Object.assign(this.time, data.time)
        
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }
};
</script>
