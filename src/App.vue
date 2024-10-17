<template>
  <div id="app" class="container mt-2">
    <!-- Countdown Card -->
    <div class="card text-center">
      <div
        class="card-header d-flex align-items-center justify-content-between"
      >
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
          Time passed since our special day! <strong>06/10/2024</strong>
        </h5>

        <!-- vue2-flip-countdown component used for count-up -->
        <flip-countdown
          :deadline="deadline"
          :showDays="true"
          @timeElapsed="timeElapsedHandler"
        ></flip-countdown>
      </div>
    </div>
  </div>
</template>

<script>
import FlipCountdown from "vue2-flip-countdown";
import moment from "moment";

export default {
  name: "app",
  components: {
    FlipCountdown,
  },
  data() {
    return {
      // Start date (October 6, 2024)
      startDate: moment("2024-10-06").valueOf(), // Fixed start date in timestamp
      deadline: moment().add(100, "years").valueOf(), // Fake future deadline (countdown will never reach this date)
      elapsedTime: 0, // Time elapsed in seconds
    };
  },
  mounted() {
    // Start interval to update elapsed time every second
    this.timer = setInterval(() => {
      this.updateElapsedTime();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer); // Clear the timer when the component is destroyed
  },
  methods: {
    updateElapsedTime() {
      const now = moment().valueOf(); // Get the current timestamp
      const diffInMilliseconds = now - this.startDate; // Calculate difference since start date

      // Convert milliseconds to seconds
      this.elapsedTime = Math.floor(diffInMilliseconds / 1000);

      // Update deadline to make it look like a count-up by shifting the deadline dynamically
      this.deadline = moment().add(this.elapsedTime, "seconds").valueOf();
    },
    timeElapsedHandler() {
      // Handle the time elapsed event if needed
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
