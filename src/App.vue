<template>
  <div id="app">
    <header><h1>Pokémon TCG</h1></header>
    Search For Cards By <select v-on:change="changeMode" v-model="searchMode">
      <option value="name" selected>Name</option>
      <option value="artist">Artist</option>
      <option value="nationalPokedexNumber">Pokédex Number</option>
      <option value="set">Set</option>
      <option value="number">Card Number</option>
    </select>:
    <input type="text" v-model="search" placeholder="Search for Cards..." v-on:keyup="searchForCard">
    <p v-if="!cards.length"> Please Enter A Valid Search (Cards Will Be Shown Below)</p>
    <span>
      <p>Found Cards: <card-list :cards="cards" /></p>
          <card-detail
           v-if="selectedCard"
            :card="selectedCard"
          ></card-detail>
    </span>
  </div>
</template>

<script>
import { eventBus } from './main.js';
import cardList from './components/cardList.vue'
import cardDetail from './components/cardDetail.vue'
import cardListItem from './components/cardListItem.vue'

export default {
  name: 'App',
  components: {
    "card-list": cardList,
    "card-list-item": cardListItem,
    "card-detail": cardDetail
  },
  data(){
    return{
      cards: [],
      "search": "",
      "searchMode": "name",
      selectedCard: null
    }
  },
  computed:{

  },
  methods:{
    changeMode: function() {
      if (this.search.length > 0){
        this.searchForCard()
      }
    },
    searchForCard: function() {
      var pages = [];
      for (var i = 1; i <= 2; i++) {
        pages.push(i);
      }
      //can go up to 122
      const promises = pages.map(num =>{
        return fetch(`https://api.pokemontcg.io/v1/cards?${this.searchMode}=${this.search.toLowerCase()}&page=${num}`)
        .then(response => response.json());
      });

      Promise.all(promises)
      .then(data => {
        const cardData = data.reduce(
          (flat, toFlatten) => flat.concat(toFlatten.cards),
          []
        );
        this.cards = cardData;
      })
      .then(() => this.sortCards("name"))
      .catch(error=> console.log(error));
    },

    sortCards: function(property) {
      this.cards.sort((a, b) => a[property] < b[property] ? -1 : 1)
    },
    
  },
  mounted(){
    // this.searchForCard();
    
    eventBus.$on("card-selected", card => (this.selectedCard = card));

  },
}
</script>

<style lang="css" scoped>
#app {
  background-color: #6EC3F4;
}

#list-info {
  display: flex;
}
</style>