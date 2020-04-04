<template lang="html">
  <div class="cardlistitem">
    <p>{{ card.name }}</p>
      <div id="picture">
        <img :src="card.imageUrl" :alt="card.name">
      </div>
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
  }
};
</script>

<style lang="css" scoped>
.cardlistitem {
  display: flex;
  font-size: 90%;
  flex-direction: column;
  padding: 10px;
  align-items: center;
  width: 200px;
  height: 300px;
  border-radius: 25px;
  border: 2px solid dodgerblue;
  background-color: white;
}

button {
  display: flex;
  font: bold 11px Futura;
  text-decoration: none;
  background-color: #EEEEEE;
  color: #333333;
  /* padding: 2px 6px 2px 6px; */
  border-top: 1px solid #CCCCCC;
  border-right: 1px solid #333333;
  border-bottom: 1px solid #333333;
  border-left: 1px solid #CCCCCC;
}

img {
  height: 80%;
  width: 80%;
  padding-left: 10px;
}    
</style>
