<script setup>
import { ref, reactive, computed, onMounted } from 'vue'
import CardComponent from '@/components/CardComponent.vue'
const all = ref(true)
const allCoffee = reactive([])
const showCoffee = computed(() =>
  all.value ? allCoffee : allCoffee.filter((item) => item.available !== false),
)

onMounted(async () => {
  try {
    let response = await fetch(
      'https://raw.githubusercontent.com/devchallenges-io/web-project-ideas/main/front-end-projects/data/simple-coffee-listing-data.json',
    )
    let data = await response.json()
    allCoffee.push(...data)
  } catch (error) {
    console.error(error)
  }
})
</script>
<template>
  <main>
    <div>
      <h1>Our Collection</h1>
      <p>
        Introducing our Coffee Collection, a selection of unique coffees from different roast types
        and origins, expertly roasted in small batches and shipped fresh weekly.
      </p>
      <img src="@/assets/Icons/vector.svg" class="vector" />
    </div>
    <div class="d-flex">
      <button :class="[all ? 'bg-button' : '']" @click="all = true">All Products</button>
      <button :class="[!all ? 'bg-button' : '']" @click="all = false">Available Now</button>
    </div>
    <div class="grid">
      <div v-for="coffee in showCoffee" :key="coffee">
        <CardComponent :obj="coffee" />
      </div>
    </div>
  </main>
</template>
<style scoped>
div {
  position: relative;
}
.vector {
  position: absolute;
  left: 45%;
  top: -20%;
  z-index: -2;
}

main {
  width: 50%;
  margin: 0 auto;
  padding: 5%;
  color: #fef7ee;
  background-color: #1b1d1f;
}
h1 {
  text-align: center;
  font-size: 2rem;
}
p {
  text-align: center;
  color: #6f757c;
  font-size: 1rem;
  width: 80%;
  margin: auto;
}
button {
  border-style: none;
  border-radius: 5px;
  margin-inline: 5px;
  padding: 1% 2%;
  background-color: transparent;
  color: #fef7ee;
}
.d-flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-block: 1%;
}
.bg-button {
  background-color: #6f757c;
}
.grid {
  display: grid;
  width: 100%;
  height: 100%;
  grid-template-columns: repeat(1, 1fr);
  gap: 10px;
}
@media screen and (min-width: 1024px) {
  p {
    width: 60%;
  }
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media screen and (min-width: 1280px) {
  p {
    width: 50%;
  }
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
