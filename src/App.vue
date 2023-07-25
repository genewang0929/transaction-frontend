<template>
  <div class="container mt-4">
    <h1>Transaction Monitor</h1>
    <div class="input-group mb-3">
      <div class="col-sm-1 col-form-label">
        <label class="my-auto">User Iban:</label>
      </div>
      <div class="col my-auto">
        <select class="form-select" aria-label="user">
          <option selected>Select user</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>
    </div>
    <button class="btn btn-success m-3">Insert 10 records to the user</button>
    <button class="btn btn-primary m-3">Get all records of the user</button>

    <!-- Cards -->
    <div class="row row-cols-1 row-cols-md-3">
      <div class="col mb-4" v-for="card in paginatedCards" :key="card.id">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ card.description }}</h5>
            <h5 class="card-subtitle">{{ card.amountWithCurrency }}</h5>
            <p class="card-text">{{ card.date }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Pagination -->
    <nav aria-label="Page navigation">
      <ul class="pagination justify-content-center">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <button class="page-link" @click="prevPage" :disabled="currentPage === 1">Previous</button>
        </li>
        <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: currentPage === page }">
          <button class="page-link" @click="gotoPage(page)">{{ page }}</button>
        </li>
        <li class="page-item" :class="{ disabled: currentPage === totalPages }">
          <button class="page-link" @click="nextPage" :disabled="currentPage === totalPages">Next</button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const cards = ref([])
const CARDS_PER_PAGE = 12
const currentPage = ref(1)

const initCards = () => {
  let cardObj = {
    id: 'fbfe820f-f017-4428-93cb-a18af834f4c6',
    iban: 'MD130V0JGFQUND01H9MJJB0C',
    description: 'Investment',
    amountWithCurrency: 'ARS 78',
    date: '2022-07-12'
  }
  for (let i = 0; i < 20; i++)
    cards.value.push(cardObj)
}

const paginatedCards = computed(() => {
  const startIndex = (currentPage.value - 1) * CARDS_PER_PAGE;
  const endIndex = startIndex + CARDS_PER_PAGE;
  return cards.value.slice(startIndex, endIndex);
})

const totalPages = computed(() => {
  return Math.ceil(cards.value.length / CARDS_PER_PAGE);
})

const gotoPage = (pageNumber) => {
  currentPage.value = pageNumber
}

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
}

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
}


initCards()
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
