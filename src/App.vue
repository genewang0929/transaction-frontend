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
    <!-- <div class="card">
      <div class="card-body">
        <h5 class="card-title">Investment</h5>
        <h6 class="card-subtitle mb-2 text-muted">ARS 78</h6>
        <p class="card-text">2022-07-12</p>
      </div>
    </div> -->
    <div class="row row-cols-1 row-cols-md-3">
      <div class="col mb-4" v-for="card in cards" :key="card.id">
        <div class="card">
          <img :src="card.imageUrl" class="card-img-top" alt="Card Image">
          <div class="card-body">
            <h5 class="card-title">{{ card.title }}</h5>
            <h5 class="card-subtitle">{{ card.subtitle }}</h5>
            <p class="card-text">{{ card.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>


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
