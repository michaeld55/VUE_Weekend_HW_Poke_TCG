<template>
  <div id="app">
    <p v-if="!cards.length"> LOADING... </p>
    <p>List of Cards: <card-list :cards="cards" /></p>
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
    "card-list-item": cardListItem
  },
  data(){
    return{
      cards: [],
      selectedCard: null
    }
  },
  computed:{

  },
  methods:{
    getCards: function() {
      const promises = [1,2,3].map(num =>{
        return fetch((`https://api.pokemontcg.io/v1/cards?page=${num}`)
        ).then(response => response.json());
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
      this.cards.sort((a, b) => {
        return a[property] < b[property] ? -1 : 1;
      });
    },
  },
  mounted(){
    this.getCards();

  },
}
</script>


