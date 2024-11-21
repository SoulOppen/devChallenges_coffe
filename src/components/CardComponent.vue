<script setup>
import { defineProps } from 'vue'
import Star_fill from '@/assets/Icons/Star_fill.svg'
import Star from '@/assets/Icons/Star.svg'
const prop = defineProps({
  obj: {
    type: Object,
    required: true,
  },
})
</script>
<template>
  <div class="card">
    <img :src="prop.obj.image" :alt="prop.obj.name" />
    <p v-if="prop.obj.popular" class="popular">Popular</p>
    <div class="card__header">
      <h2>{{ prop.obj.name }}</h2>
      <p class="card__price">{{ prop.obj.price }}</p>
    </div>
    <div class="d-flex">
      <div class="card__footer">
        <div class="star">
          <img :src="prop.obj.votes > 0 ? Star_fill : Star" alt="Star Icon" />
        </div>
        <p v-if="prop.obj.votes > 0">
          <span class="rating">{{ prop.obj.rating }}</span>
          ({{ prop.obj.votes }} votes)
        </p>
        <p v-else>No votes</p>
      </div>
      <p v-if="prop.obj.votes > 0 && !prop.obj.available" class="sold">Sold Out</p>
    </div>
  </div>
</template>
<style scoped>
.card {
  position: relative;
  margin: 0 auto;
  width: 100%;
  padding: 1%;
}
img {
  display: block;
  width: 100%;
  margin: auto;
  border-radius: 5px;
}
p {
  color: #6f757c;
}
.popular {
  position: absolute;
  top: 1%;
  left: 1%;
  color: #111315;
  background-color: #f6c768;
  width: fit-content;
  border-radius: 10%;
  padding: 1% 2%;
  font-size: 0.875rem;
  font-weight: bold;
}
.card__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-block: 2.5%;
}
.card__price {
  background-color: #bee3cc;
  color: #1b1d1f;
  border-radius: 10%;
  padding: 1% 2%;
  font-weight: bold;
}
.card__footer {
  display: flex;
  align-items: center;
}
.d-flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.rating {
  color: #bee3cc;
}

.star {
  width: 20%;
  flex: 1;
}
.sold {
  color: #ed735d;
}
</style>
