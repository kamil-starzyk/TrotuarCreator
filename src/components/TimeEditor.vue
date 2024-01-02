<template>
  <div>
    <h1>Time Details</h1>
    <div v-if="time">
      <p>Seconds: {{ time.s }}</p>
      <p>Minutes: {{ time.m }}</p>
      <p>Hours: {{ time.h }}</p>
      <!-- Display other time properties -->
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    time: Object // Define time as a prop
  }
};
</script>
