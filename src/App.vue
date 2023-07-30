<template>
  <div class="container mt-4">
    <h1>Transaction Monitor</h1>
    <div class="input-group mb-3">
      <div class="col-sm-1 col-form-label">
        <label class="my-auto">User Iban:</label>
      </div>
      <div class="col my-auto">
        <select v-model="selectedUser" class="form-select" aria-label="user">
          <option v-for="user in users" :key="user.iban">
            {{ user.iban }}
          </option>
        </select>
      </div>
    </div>
    <button class="btn btn-success m-3" @click="insertTenRecords">Insert 10 records to the user</button>
    <button class="btn btn-primary m-3" @click="getUserTransaction(selectedUser, currentPage, CARDS_PER_PAGE)">Get all records of the user</button>

    <!-- Cards -->
    <div class="row row-cols-1 row-cols-md-3">
      <div class="col mb-4" v-for="card in cards" :key="card.id">
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
import { ref } from 'vue';
import axios from 'axios';

const users = ref([])
const selectedUser = ref('')
const cards = ref([])
const CARDS_PER_PAGE = 12
const currentPage = ref(1)
const totalPages = ref(1)

const getAllUsers = async () => {
  try {
    const response = await axios.get(`/api/user`)
    users.value = response.data.transaction
  } catch (error) {
    console.error(error)
  }
}

const getUserTransaction = async (userIban, currentPage, CARDS_PER_PAGE) => {
  try {
    const response = await axios.get(`/api/bankTransaction/${userIban}/${currentPage - 1}/${CARDS_PER_PAGE}`)
    cards.value = response.data.transactions.content
    totalPages.value = response.data.transactions.totalPages
  } catch (error) {
    console.error(error)
  }
}

const insertTenRecords = async () => {
  try {
    const response = await axios.post(`/api/bankTransaction?iban=${selectedUser.value}`)
    console.log(response)
  } catch (error) {
    console.error(error)
  }
}

const gotoPage = (pageNumber) => {
  currentPage.value = pageNumber
  getUserTransaction(selectedUser.value, currentPage.value, CARDS_PER_PAGE)
}

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
  getUserTransaction(selectedUser.value, currentPage.value, CARDS_PER_PAGE)
}

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
  getUserTransaction(selectedUser.value, currentPage.value, CARDS_PER_PAGE)
}


getAllUsers()
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
