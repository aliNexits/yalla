<template>
  <div id="app" class="container mt-2">
    <!-- Count-Up Card -->
    <div class="card text-center">
      <div class="card-header d-flex align-items-center justify-content-between">
        <img
          src="../images/avatar.jpg"
          class="rounded-circle"
          alt="Avatar 1"
          style="width: 100px; height: 100px"
        />

        <!-- Title -->
        <h3 class="mx-3">🎉🥳<strong>Save The Date</strong>🎉🥳</h3>

        <!-- Avatar After -->
        <img
          src="../images/avatar1.png"
          class="rounded-circle"
          alt="Avatar 2"
          style="width: 100px; height: 100px"
        />
      </div>
      <div class="card-body">
        <h5 class="card-title">
          Time passed since our special day!!!! <strong>06/10/2024</strong>
        </h5>

        <!-- Timer Component to display count-up -->
        <Timer :years="time.years" :days="time.days" :hours="time.hours" :minutes="time.minutes" :seconds="time.seconds" />
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import Timer from "./Timer.vue"; // Import the Timer component

export default {
  name: "app",
  components: {
    Timer, // Register the Timer component
  },
  data() {
    return {
      // Fixed start date (October 6, 2024)
      startDate: moment("2024-10-06").valueOf(),
      elapsedTime: 0, // Time elapsed in seconds
    };
  },
  computed: {
    time() {
      const now = moment();
      const duration = moment.duration(now.diff(this.startDate)); // Get the duration

      return {
        years: Math.floor(duration.asYears()), // Calculate years
        days: Math.floor(duration.asDays()) % 365, // Calculate remaining days
        hours: now.hours(), // Current hour
        minutes: now.minutes(), // Current minute
        seconds: now.seconds(), // Current second
      };
    },
  },
  mounted() {
    // Start updating the elapsed time every second
    this.timer = setInterval(() => {
      this.updateElapsedTime();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer); // Clear the timer when the component is destroyed
  },
  methods: {
    updateElapsedTime() {
      // No longer needed since we use the computed property
    },
  },
};
</script>










<style>
body {
  position: relative;
  margin: 0;
  height: 100vh;
  overflow: hidden;
}

body::after {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: url("../images/avatar2.jpg") no-repeat center center;
  background-size: cover;
  opacity: 0.7; /* Light opacity */
  z-index: -1;
}

#app {
  background-color: rgba(
    255,
    255,
    255,
    0.85
  ); /* Light opacity background for readability */
  padding: 20px;
  border-radius: 8px;
  max-width: 900px;
  margin: auto;
  position: relative;
  z-index: 1;
}

.carousel-item img {
  max-height: 400px;
  object-fit: cover;
}
</style>
