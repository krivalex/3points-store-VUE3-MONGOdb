<template>
  <div>
    <div class="cards">
      <OneCard v-for="card in cards" :key="card.id" :id="card.id" :name="card.name" :size_eu="card.size_eu"
        :color="card.color" :link="card.link" :image="card.image"></OneCard>
    </div>

  </div>
</template>
<script>
import OneCard from './OneCard.vue'
import snickers_data from './data'

export default {
  name: 'ManyCard',
  components: OneCard,
  data() {
    return {
      cards: snickers_data
    }
  }

}
</script>

<style>

</style>
