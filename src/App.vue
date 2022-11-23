<template>
  <v-app>
    <v-app-bar app color="blue-grey" dark>
      <div class="d-flex align-center">
        <h2>SpaceX Timeline</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-timeline v-if="launches.length">
          <LaunchTimelineItem
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import LaunchTimelineItem from "./components/LaunchTimelineItem.vue";

export default {
  name: "App",

  components: { LaunchTimelineItem },
  data() {
    return {
      launches: [],
    };
  },
  async created() {
    const res = await fetch("https://api.spacexdata.com/v3/launches");
    const data = await res.json();
    data.forEach((launch) => {
      this.launches.push(launch);
    });
    console.log(this.launches);
  },
};
</script>
