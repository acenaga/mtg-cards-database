<template>
    <div class="container-fluid">
        <div class="row justify-content-center">
            <div class="col-12 col-lg-4 ">
                <p>Choosed: {{ chooseApi }}</p>
                <input class="form-check-input" type="radio" value="1" v-model="chooseApi" id="chooseApi1">
                <label class="form-check-label" for="chooseApi1">
                    Api Magic the Gathering
                </label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" value="2" v-model="chooseApi" id="chooseApi2" checked>
                <label class="form-check-label" for="chooseApi2">
                    SCy fall
                </label>
                <form class="d-flex">
                    <input class="form-control me-2" v-model="cardSearch" type="search" placeholder="Search"
                        aria-label="Search">
                    <button class="btn btn-outline-success" @click.prevent="searchingCard()" type="submit">Search</button>
                </form>
            </div>
        </div>

    </div>
</template>

<script>
import axios from "axios";
export default {
    name: 'SearchForm',
    data() {
        return {
            cardSearch: '',
            responseApi: {},
            chooseApi: '2'

        }
    },
    methods: {
        searchingCard() {

        },
        async searchCard() {
            const options = {
                method: "GET",
                url: "https://api.magicthegathering.io/v1/cards",
                params: {
                    name: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);
            this.responseApi = response;
            this.$emit('search', this.responseApi);
        },
        async searchCardScryfall() {
            const options = {
                method: "GET",
                url: "https://api.scryfall.com",
                params: {
                    name: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);
            this.responseApi = response;
            this.$emit('search', this.responseApi);
        },
        async searchCardTgcPlayer() {
            const options = {
                method: "GET",
                url: "https://api.magicthegathering.io/v1/cards",
                params: {
                    name: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);
            this.responseApi = response;
            this.$emit('search', this.responseApi);
        },

    }
}

</script>