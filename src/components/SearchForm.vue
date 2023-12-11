<template>
    <div class="container-fluid">
        <div class="row justify-content-center">
            <div class="col-12 col-lg-4  d-flex flex-column align-items-center">
                <p>Choosed: {{ chooseApi }}</p>
                <div class="form-check">
                    <input class="form-check-input" type="radio" value="1" v-model="chooseApi" id="chooseApi1" checked>
                    <label class="form-check-label" for="chooseApi1">
                        Magic The gathering IO
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="radio" value="2" v-model="chooseApi" id="chooseApi2">
                    <label class="form-check-label" for="chooseApi2">
                        Scry Fall
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="radio" value="3" v-model="chooseApi" id="chooseApi3">
                    <label class="form-check-label" for="chooseApi3">
                        Tgc Player
                    </label>
                </div>
                <div>
                    <div class="form-check form-check-inline">
                        <input class="form-check-input" type="radio" v-model="chooseType" id="inlineRadio1" value="cards">
                        <label class="form-check-label" for="inlineRadio1" checked>Cards</label>
                    </div>
                    <div class="form-check form-check-inline">
                        <input class="form-check-input" type="radio" v-model="chooseType" id="inlineRadio2" value="sets">
                        <label class="form-check-label" for="inlineRadio2">sets</label>
                    </div>
                </div>
            </div>
            <div class="form-check">
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
            chooseApi: 1,
            chooseType: 'cards',
            cardName: '',
            legality: '',
            price: '',
            image: '',
            imageFlip: '',
            ruling: '',
            type: '',
            subType: '',
            rarity: '',
            set: '',
            setName: '',

        }
    },
    methods: {
        searchingCard() {

            // console.log(this.chooseApi);
            if (this.chooseApi == 1) {
                this.searchCardMagigIo();
            } else if (this.chooseApi == 2) {
                this.searchCardScryfall();
            } else if (this.chooseApi == 3) {
                this.searchCardTgcPlayer();
            }

        },
        async searchCardMagigIo() {
            const options = {
                method: "GET",
                url: "https://api.magicthegathering.io/v1/" + this.chooseType,
                params: {
                    name: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);

            console.log(response.data);
            this.responseApi = response.data.cards;
            this.magicTheGatheringIo(this.responseApi);

        },
        async searchCardScryfall() {
            // TODO read about scryfall api
            const options = {
                method: "GET",
                url: "https://api.scryfall.com" + "/cards/named",
                params: {
                    fuzzy: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);
            console.log(response.data);
            // this.responseApi = response;
            // this.$emit('search', this.responseApi);
        },
        async searchCardTgcPlayer() {
            const options = {
                method: "GET",
                url: "https://api.magicthegathering.io/v1/" + this.chooseType,
                params: {
                    name: this.cardSearch,
                },
                headers: {
                    "Content-Type": "application/json",
                },
            };
            const response = await axios(options);
            this.responseApi = response.data.cards;
            console.log(this.responseApi);
            // this.$emit('search', this.responseApi);
        },

        magicTheGatheringIo(response) {

            response.forEach(element => {
                this.cardName = element.name;
                this.legality = element.legalities;
                this.price = element.prices;
                this.image = element.imageUrl;
                this.imageFlip = element.imageFlipUrl;
                this.ruling = element.rulings;
                this.type = element.type;
                this.subType = element.subType;
                this.rarity = element.rarity;
                this.set = element.set;
                this.setName = element.setName;
            });


            this.$emit('search', response);
        },

        tgcPlayer(response) {
            console.log(response);
            // response.forEach(element => {
            //     this.cardName = element.name;
            //     this.legality = element.legalities;
            //     this.price = element.prices;
            //     this.image = element.imageUrl;
            //     this.imageFlip = element.imageFlipUrl;
            //     this.ruling = element.rulings;
            //     this.type = element.type;
            //     this.subType = element.subType;
            //     this.rarity = element.rarity;
            //     this.set = element.set;
            //     this.setName = element.setName;
            // });


            //this.$emit('search', response);
        },

    }
}

</script>