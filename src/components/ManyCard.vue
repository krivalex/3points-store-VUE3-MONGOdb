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
  components: { OneCard },
  data() {
    return {
      cards: snickers_data
    }
  }

}
</script>

<style>
.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100%;
  padding: 0 10px;
}

.cards .one-card {
  width: 30%;
  height: 300px;
  margin: 10px 0;
}
</style>
