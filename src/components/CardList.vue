<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 col-md-4 col-lg-3 p-3" v-for="card in cards" :key="card.id">
                <div class="accordion" :id="'accordionExample' + card.id">
                    <div class="accordion-item">
                        <h2 class="accordion-header" :id="'headingOne' + card.id">
                            <button class="accordion-button" type="button" data-bs-toggle="collapse"
                                :data-bs-target="'#collapseOne' + card.id" aria-expanded="false"
                                :aria-controls="'collapseOne' + card.id">
                                {{ card.name }}
                                <img class="w-50" :src="card.imageUrl" :alt="card.name">
                            </button>
                        </h2>
                        <div :id="'collapseOne' + card.id" class="accordion-collapse collapse"
                            :aria-labelledby="'headingOne' + card.id" :data-bs-parent="'#accordionExample' + card.id">
                            <div class="accordion-body">
                                <img :src="card.imageUrl" :alt="card.name">
                                <p>Name: {{ card.name }}</p>
                                <div v-if="card.names">
                                    <p v-for="name in card.names" :key="name.id">
                                        {{ name }}
                                    </p>

                                </div>
                                <p>Artist: {{ card.artist }}</p>
                                <p>Layout: {{ card.layout }}</p>
                                <p>Converted mana cost: {{ card.cmc }}</p>
                                <div v-if="card.colors">
                                    <h5>The card colors:</h5>
                                    <!-- eslint-disable-next-line vue/require-v-for-key -->
                                    <p v-for="color in card.colors" :key="color.key">
                                        {{ color }}
                                    </p>
                                </div>
                                <div v-if="card.colorIdentity">
                                    <h5>The card’s color identity: </h5>
                                    <p v-for="identity in card.colorIdentity" :key="identity.key">
                                        {{ identity }}
                                    </p>

                                </div>
                                <p>The card type: {{ card.type }}</p>
                                <div v-if="card.supertypes">
                                    <h5>The supertypes of the card:</h5>
                                    <p v-for="supertype in card.supertypes" :key="supertype.id">
                                        {{ supertype }}
                                    </p>

                                </div>
                                <div v-if="card.types">
                                    <h5>The types of the card:</h5>
                                    <p v-for="type in card.types" :key="type.id">
                                        {{ type }}
                                    </p>

                                </div>
                                <div v-if="card.subtypes">
                                    <h5>The subtypes of the card:</h5>
                                    <p v-for="subtype in card.subtypes" :key="subtype.id">
                                        {{ subtype }}
                                    </p>
                                </div>
                                <p>The card rarity: {{ card.rarity }}</p>
                                <p>The set the card belongs to (set code): {{ card.set }}</p>
                                <p>The set the card belongs to: {{ card.setName }}</p>
                                <p>The oracle text of the card: {{ card.text }}</p>
                                <p v-if="card.flavor">The flavor text of the card: {{ card.flavor }}</p>
                                <p>The card number: {{ card.number }}</p>
                                <p>The card power: {{ card.power }}</p>
                                <p>The card toughness: {{ card.toughness }}</p>
                                <p>The card loyalty: {{ card.loyalty }}</p>
                                <p v-if="card.language">The language the card is printed in: {{ card.language }}</p>
                                <p>The card multiverse id: {{ card.multiverseid }}</p>
                                <div v-if="card.printings">
                                    <h5>The sets the card is printed in:</h5>
                                    <p v-for="print in card.printings" :key="print.id">
                                        {{ print }}
                                    </p>
                                </div>
                                <div v-if="card.rulings">
                                    <h5>The rulings of the card:</h5>
                                    <p v-for="ruling in card.rulings" :key="ruling.id">
                                        {{ ruling.date }}: {{ ruling.text }}
                                    </p>

                                </div>

                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'CardList',
    props: {
        cards: {
            type: Object,
            required: true
        }
    }
}
</script>