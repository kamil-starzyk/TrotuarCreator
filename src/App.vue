<template>
  <div id="app">
    <div v-if="time">
      <TimeEditor :time="time" @change="(time) => Object.assign(this.time, time)"/>
      {{ JSON.stringify(time) }}
      </div>
    <div v-else>
      <p>Loading...</p>
    </div>
    <!-- Other components using specific data -->

    <br>
    <button @click="downloadJSON">Zrzuć JSONa</button>
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
  },
  methods: {
    downloadJSON() {
      // eslint-disable-next-line no-unused-vars
      const {isTrusted, _vts, ...rest} = this.time
      const jsonData = JSON.stringify({...this.gameData, time:rest});

      // Create a Blob object to store the JSON data
      const blob = new Blob([jsonData], { type: "application/json" });

      // Create a temporary anchor element
      const link = document.createElement("a");
      link.href = window.URL.createObjectURL(blob);

      // Set the filename for the downloaded JSON file
      link.download = "game_data.json";

      // Trigger the click event to download the JSON file
      link.click();

      // Cleanup
      window.URL.revokeObjectURL(link.href);
    }
  }
};
</script>
