<template lang="html">
  <div class="cardlistitem">
    <p>{{ card.name }}</p>
    <button v-on:click="displayInfo">More Info &rarr;</button>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";

export default {
  name: "card-list-item",
  props: ["card"],
 
  methods: {
    displayInfo: function() {
      eventBus.$emit("card-selected", this.card);
    },

    addFavourite: function() {
      eventBus.$emit("favourite-added", this.card);
    },

    removeFavourite: function() {
      eventBus.$emit("favourite-removed", this.card);
    }
  }
};
</script>

<style lang="css" scoped>

</style>
