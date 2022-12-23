<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-lg-4">
        <figure class="d-flex flex-column justify-content-center">
          <img class="w-50" alt="Magic the gathering Logo" src="./assets/logo.png">
          <figcaption>Your database Search</figcaption>
        </figure>
      </div>
    </div>
    <SearchForm @search="showResponse" />
    <CardList :cards="responseCards" />

  </div>


</template>

<script>
import SearchForm from './components/SearchForm.vue'
import CardList from './components/CardList.vue';

export default {
  name: 'App',
  components: {
    SearchForm,
    CardList
  },
  data() {
    return {
      responseApi: {},
      responseCards: {},
      responseHeader: {}
    }
  },
  methods: {
    showResponse(response) {
      console.log('para el header');
      console.log(response.headers)
      console.log('para las cards');
      console.log(response.data.cards);
      this.responseHeader = response.headers;
      this.responseCards = response.data.cards;
    }
  }
}
</script>


