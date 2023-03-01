<template>
    <div class="container-fluid">
        <div class="row justify-content-center">
            <div class="col-12 col-lg-4 ">
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
            responseApi: {}

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