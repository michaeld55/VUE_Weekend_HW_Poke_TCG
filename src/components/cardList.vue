<template lang='html'>
<div class="card-list" v-if="cards.length">
    <card-list-item
        v-for="(card, index) in cards"
            :card="card"
            :key="index"
    >
    </card-list-item>
</div>
  
</template>

<script>
import { eventBus } from '../main.js';
import cardListItem from '@/components/cardListItem.vue';


export default {
    name: "cardlist",
    props: ["cards"],
    components: {
        "card-list-item": cardListItem
    },
    methods:{

    }

}
</script>

<style scoped>

</style>