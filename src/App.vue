<template>
  <div id="app">
    <TimeEditor :time="timeData.time" />
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
      timeData: null // Initialize data object to store time data
    };
  },
  created() {
    // Load demo.json and fetch necessary data
    fetch('data/demo.json') // Adjust the path as needed
      .then(response => response.json())
      .then(data => {
        this.timeData = data; // Store the entire data object from demo.json
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }
};
</script>
