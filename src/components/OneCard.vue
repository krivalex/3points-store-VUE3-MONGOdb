<template>
  <div class="one-card">
    <div class="card-image">
      <img crossorigin="anonymous" :src="require(`@/assets/photos/${id}.jpg`)" alt="image">
    </div>
    <div class="card-info">
      <h2>{{ name }}</h2>
      <p>Размеры: {{ size_eu.map(el => el) }}</p>
      <p>Цвета: {{ color }}</p>
      <a :href="link">Подробнее</a>
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
    color: Array,
    link: String,
    image: String
  },
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
}

.one-card:hover {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.8);
  transition: 0.3s;
}

.card-image {
  width: 100%;
  height: 50%;
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

.card-info h2 {
  font-size: 20px;
  font-weight: 600;
  margin: 0;
}

.card-info p {
  font-size: 16px;
  font-weight: 400;
  margin: 0;
}

.card-info a {
  font-size: 16px;
  font-weight: 400;
  margin: 0;
  color: #0460ac;
  text-decoration: none;
  transition: 0.3s;
}

.card-info a:hover {
  color: #0b80e0;
  transition: 0.3s;
}
</style>
