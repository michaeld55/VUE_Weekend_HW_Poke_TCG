<template>
  <div id="card-detail-container">
    <div id="card-detail">
      <div id="picture">
        <img :src="card.imageUrlHiRes" :alt="card.name">
      </div>
      <div id="card-text">
        <ul>
          <li>{{card.supertype}} Card Name: {{card.name}}</li>
          <li v-if="card.types">Card Types: {{card.types[0]}}{{card.types[1]}}</li>
          <li v-if="card.evolvesFrom">Previous Evolution: {{card.evolvesFrom}}</li>
          <li v-if="card.nationalPokedexNumber">Pokédex Number: {{card.nationalPokedexNumber}}</li>
          <li v-if="card.subtype">Card Type: {{card.subtype}}</li>
          <li v-if="card.text"> Card Special Text: {{card.text[0]}}</li>
          <li>Card Rarity: {{card.rarity}}</li>
          <li>Card Series: {{card.series}}</li>
          <li>Card Set: {{card.set}}</li>
          <li>Card Number: {{card.number}}</li>
          <li>Card Aritist: {{card.artist}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js';


export default {
    name: "list",
    props: ["card"],
    methods:{

    }

}
</script>

<style scoped>
#card-detail-container {
  width: 90%;
}

#card-detail {
  display: flex;
}

p {
  font: 25px Ariel;
}

li {
  list-style: none;
  font: 25px Ariel;
}

#picture {
  display: flex;
  flex-direction: column;
  padding: 20px;
}

#attacksContainer {
  display: flex;
  justify-content: space-evenly;
  padding-bottom: 60px;
}

#card-text {
  margin-left: 10%;
  margin-right: 10%;
  word-wrap: normal;
}


h3 {
  font: bold 15px Futura;
}

.attacks {
  padding-left: 15px;
  padding-right: 30px;
  border-radius: 25px;
  border: 2px solid dodgerblue;
  background-color: white;
}
</style>