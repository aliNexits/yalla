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
          Countdown to our special day! <strong>06/10/2024</strong>
        </h5>

        <flip-countdown
      :startTime="startTime"
      :showDays="true"
      @timeElapsed="timeElapsedHandler"
    ></flip-countdown>
      </div>
    </div>

    <!-- Image Carousel -->
    <div
      style="border-radius: 30px"
      id="imageCarousel"
      class="carousel slide mt-2"
      data-ride="carousel"
      data-interval="3000"
    >
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img
            style="border-radius: 30px"
            src="../images/cr.jpg"
            class="d-block w-100"
            alt="Image 1"
          />
        </div>
        <div class="carousel-item">
          <img
            style="border-radius: 30px"
            src="../images/cr4.jpg"
            class="d-block w-100"
            alt="Image 2"
          />
        </div>
        <div class="carousel-item">
          <img
            style="border-radius: 30px"
            src="../images/cr3.jpg"
            class="d-block w-100"
            alt="Image 3"
          />
        </div>
        <div class="carousel-item">
          <img
            style="border-radius: 30px"
            src="../images/cr1.jpg"
            class="d-block w-100"
            alt="Image 4"
          />
        </div>
        <div class="carousel-item">
          <img
            style="border-radius: 30px"
            src="../images/cr5.jpg"
            class="d-block w-100"
            alt="Image 5"
          />
        </div>
        <div class="carousel-item">
          <img
            style="border-radius: 30px"
            src="../images/avatar2.jpg"
            class="d-block w-100"
            alt="Image 5"
          />
        </div>
      </div>
      <a
        class="carousel-control-prev"
        href="#imageCarousel"
        role="button"
        data-slide="prev"
      >
        <span class="carousel-control-prev-icon"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a
        class="carousel-control-next"
        href="#imageCarousel"
        role="button"
        data-slide="next"
      >
        <span class="carousel-control-next-icon"></span>
        <span class="sr-only">Next</span>
      </a>
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
      // Set startDayTs to the timestamp of October 6, 2024
      startDayTs: moment("2024-10-06").valueOf(), // Fixed start date
      currentTimestamp: moment().valueOf(), // Current timestamp
    };
  },
  computed: {
    startTime: function () {
      const diff = this.currentTimestamp - this.startDayTs; // Time difference in milliseconds
      return moment.utc(diff).format("YYYY-MM-DD HH:mm:ss"); // Convert difference to readable format
    },
  },
  mounted() {
    // Update the time every second
    this.timer = setInterval(() => {
      this.currentTimestamp = moment().valueOf(); // Update current time
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer); // Clear the timer when the component is destroyed
  },
  methods: {
    timeElapsedHandler: function () {
      // Handle any event when time is being tracked
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
