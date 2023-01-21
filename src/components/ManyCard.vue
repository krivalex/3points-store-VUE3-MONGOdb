<template>
  <div v-if="filterData.length > 0" class="cards">
    <div v-for="card in filterData" :key="card.id">
      <OneCard :key="card.id" :id="card.id" :name="card.name" :size_eu="card.size_eu" :colors="card.color"
        :link="card.link" :image="card.image"></OneCard>
    </div>
  </div>
  <div v-else-if="size_eu + 0.5 < 36 || size_eu > 46" id="not-size" class="cards">
    <h2>У нас нет такого размера😞</h2>
  </div>
  <div v-else id="not-color" class="cards">
    <h2>У нас нет такого цвета, под ваш размер😞</h2>
  </div>
</template>
<script>
import OneCard from './OneCard.vue'
import snickers_data from './data'

export default {
  name: 'ManyCard',
  props: {
    size_eu: Number,
    colors: Array,
  },
  components: { OneCard },
  methods: {
  },
  computed: {
    filterData() {
      return this.cards.filter(card => (card.size_eu.includes(this.size_eu) || card.size_eu.includes(this.size_eu + 0.5) || card.size_eu.includes(this.size_eu - 0.5)) && card.color.filter(i => this.colors.includes(i)).length > 0)
    }
  },
  data() {
    return {
      cards: snickers_data,
      intersection: [],
    }
  }

}
</script>

<style>
.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  padding: 0 10px;
  margin-top: 20px;
  text-align: center;

}

#not-found {
  font-size: 20px;
}

@media screen and (max-width: 768px) {
  .cards .one-card {
    min-width: 90%;
    height: 500px;
    margin: 10px;

  }
}

@media screen and (min-width: 768px) {
  .cards .one-card {
    width: 350px;
    height: 450px;
    margin: 10px;
  }


}
</style>
