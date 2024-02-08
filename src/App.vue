<template>
  <div id="app">
    <div v-if="gameData.time">
      <PlayerEditor :player="gameData.player" @change="(player) => Object.assign(this.gameData.player, player)"/>
      <TimeEditor :time="gameData.time" @change="(time) => Object.assign(this.gameData.time, time)"/>

      
      <pre>{{ JSON.stringify(gameData.player.equipment, null, 2) }}</pre>
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
import PlayerEditor from './components/PlayerEditor.vue'; // Import the TimeDisplay component

export default {
  components: {
    TimeEditor, // Register the TimeDisplay component
    PlayerEditor // Register the TimeDisplay component
  },
  data() {
    return {
      gameData: {}
    };
  },
  created() {
    // Load demo.json and fetch necessary data
    fetch('data/demo.json') // Adjust the path as needed
      .then(response => response.json())
      .then(data => {

        this.gameData = data; // Store the entire data object from demo.json

        Object.assign(this.gameData, data)
        console.log(this.gameData)
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  },
  methods: {
    downloadJSON() {
      // eslint-disable-next-line no-unused-vars
      const {isTrusted, _vts, ...rest} = this.gameData
      const jsonData = JSON.stringify(rest, null, 2);

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
