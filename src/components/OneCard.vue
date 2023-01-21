<template>
  <div class="one-card" @click="redirectInsta">
    <div class="card-image">
      <img crossorigin="anonymous" :src="require(`@/assets/photos/${id}.jpg`)" alt="image">
    </div>
    <div class="card-info">
      <p class="name">{{ name }}</p>
      <p class="size">Размеры: <br /> {{ size_eu.join("|") }}</p>
      <p class="color">Цвета: {{ colors.join(",") }}</p>
      <a class="link" :href="link">Подробнее</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OneCard',
  props: {
    id: Number,
    name: String,
    size_eu: Array,
    colors: Array,
    link: String,
    image: String
  },
  methods: {
    redirectInsta() {
      window.open(this.link, '_blank')
    }
  }
};

</script>

<style scoped>
.one-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  transition: 0.3s;
  width: 400px;
}

.one-card:hover {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.8);
  transition: 0.3s;
}

.card-image {
  width: 100%;
  height: 90%;
  border-radius: 10px 10px 0 0;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 50%;
  padding: 10px;
}


.card-info a {
  font-size: 16px;
  font-weight: 400;
  margin: 0;
  color: #0460ac;
  text-decoration: none;
  transition: 0.3s;
  background-color: #fff;
  border: 1px solid #0460ac;
  border-radius: 5px;
  padding: 5px 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.card-info a:hover {
  color: #0b80e0;
  transition: 0.3s;
}

.size {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  word-wrap: break-word;
  text-align: center;
  margin-top: 15px;
  margin-bottom: 15px;
}

.name {
  text-align: center;
  font-size: 30px;
  font-weight: 600;
}
</style>
