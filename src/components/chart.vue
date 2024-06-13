<template>
  <v-container class="pa-5">
    <v-row justify="center">
      <v-col cols="12" md="6">
        <v-card>
          <v-img src="https://cdn.vuetifyjs.com/images/cards/docks.jpg" height="200px"></v-img>
          <v-card-title>
            <span class="headline">อิอิ Dock</span>
          </v-card-title>
          <v-card-subtitle>Victoria, British Columbia</v-card-subtitle>
          <v-card-text>
            <div>
              <p>Experience the serene beauty of the docks in Victoria, BC. This place is a must-visit for nature lovers and photographers.</p>
              <v-divider class="my-2"></v-divider>
              <p>Distance: 2.4 km</p>
              <p>Travel Time: 15 mins</p>
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary">Learn More</v-btn>
            <v-btn color="secondary">Book Now</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'InteractiveCard',
};
</script>

<style>
/* You can add any custom styles here */
</style>
