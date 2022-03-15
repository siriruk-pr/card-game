<template>
    <div class="game-page">
        <section class="section-profile-cover section-shaped my-0">
            <div class="shape shape-style-1 shape-primary shape-skew alpha-4">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
            </div>
            <div class="container shape-container d-flex">
                <div class="col px-0">
                    <div class="row">
                        <div class="col-lg-6">
                            <h1 class="display-3 text-white">Let's Play!
                                <span>Choose one card</span>
                            </h1>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <section class="section section-lg pt-lg-0 mt--300">
            <div class="container">
                <div class="row justify-content-center">
                    <div class="col-lg-12">
                        <div class="row row-grid">
                            <div class="col-lg-3 col-md-3 col-sm-3 text-center">
                                <div v-bind:id="'d-'+cards[0].name">
                                    <card class="border-card" hover shadow body-classes="py-5" :style="{'background-color': cards[0].color_code }">
                                        <h5 class="text-uppercase display-3" :style="{'color': cards[0].txt_code }">{{ cards[0].name }}</h5>
                                        <base-button data-idn=0 v-bind:id="cards[0].name" type="secondary" :class="{'is-select': cards[0].isSelecting, 'not-select': !cards[0].isSelecting, 'mt-4': 'mt-4'}" v-on:click="select($event)">
                                            select
                                        </base-button>
                                    </card>
                                </div>
                            </div>
                            
                            <div class="col-lg-3 col-md-3 col-sm-3 text-center">
                                <div v-bind:id="'d-'+cards[1].name">
                                    <card class="border-card" hover shadow body-classes="py-5" :style="{'background-color': cards[1].color_code }">
                                        <h5 class="text-uppercase display-3" :style="{'color': cards[1].txt_code }">{{ cards[1].name }}</h5>
                                         <base-button data-idn=1 v-bind:id="cards[1].name" type="secondary" :class="{'is-select': cards[1].isSelecting, 'not-select': !cards[1].isSelecting, 'mt-4': 'mt-4'}" v-on:click="select($event)">
                                            select
                                        </base-button>
                                    </card>
                                </div>
                            </div>
                            <div class="col-lg-3 col-md-3 col-sm-3 text-center">
                                <div v-bind:id="'d-'+cards[2].name">
                                    <card class="border-card" hover shadow body-classes="py-5" :style="{'background-color': cards[2].color_code }">
                                        <h5 class="text-uppercase display-3" :style="{'color': cards[2].txt_code }">{{ cards[2].name }}</h5>
                                        <base-button data-idn=2 v-bind:id="cards[2].name" type="secondary" :class="{'is-select': cards[2].isSelecting, 'not-select': !cards[2].isSelecting, 'mt-4': 'mt-4'}" v-on:click="select($event)">
                                            select
                                        </base-button>
                                    </card>
                                </div>
                            </div>
                            <div class="col-lg-3 col-md-3 col-sm-3 text-center">
                                <div v-bind:id="'d-'+cards[3].name">
                                    <card class="border-card" hover shadow body-classes="py-5" :style="{'background-color': cards[3].color_code }">
                                        <h5 class="text-uppercase display-3" :style="{'color': cards[3].txt_code }">{{ cards[3].name }}</h5>
                                        <base-button data-idn=3 v-bind:id="cards[3].name" type="secondary" :class="{'is-select': cards[3].isSelecting, 'not-select': !cards[3].isSelecting, 'mt-4': 'mt-4'}" v-on:click="select($event)">
                                            select
                                        </base-button>
                                     </card>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="col-lg-12 mt-3 text-center vs">VS</div>
                      
                    <div class="col-lg-12 mt-3">
                        <div class="row row-grid justify-content-center">
                            <div class="col-lg-3 col-md-3 col-sm-3 text-center">
                                <div id="random">
                                    <card class="card_random" hover shadow body-classes="py-5" v-bind:style="{ 'background-color': randBgColor }">
                                        <h5 class="text-uppercase display-4">Random</h5>
                                    </card>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="col-lg-12 mt-3">
                        <!-- Modals -->
                        <modals :sel_color="results.sel_color" :rand_color="results.rand_color" :result_txt="results.result_txt" :pcount="results.pcount"></modals>
                    </div>

                </div>
            </div>
        </section>   
    </div>
</template>

<script>
import Modals from "./ResultModals";
export default {
    components: {
        Modals
    },
    data: function() {
        return  {
           cards: [
                { name: 'red', color_code: '#EB3812', txt_code: '#ecaeae', isSelecting: false },
                { name: 'blue', color_code: '#8ED5FA', txt_code: '#1C78C0', isSelecting: false },
                { name: 'green', color_code: '#BBD500', txt_code: '#708000', isSelecting: false },
                { name: 'brown', color_code: '#76470B', txt_code: '#562604', isSelecting: false }
            ],
            randBgColor: '#B2AFB3',
            results: {
                sel_color: '',
                rand_color: '',
                result_txt: '',
                pcount: 0
            }
        }
    },
    methods: {
        select: function(event) {
            var select_color = event.target.getAttribute('id');
            var idn = event.target.getAttribute('data-idn');
            var select_color_code = this.cards[idn].color_code;
    
            for (let i=0; i<this.cards.length; i++) {
                if (i == idn) {
                    this.$set(this.cards[i], 'isSelecting', true);
                } else {
                    this.$set(this.cards[i], 'isSelecting', false);
                }
            }

            // Random card
            var rand_int = this.random_card();
            var rand_color = this.cards[rand_int].name;
            var rand_color_code = this.cards[rand_int].color_code;

            this.randBgColor = this.cards[rand_int].color_code;

            // Prepare result
            var win =  this.compare_card(select_color, rand_color);

            this.results.sel_color = select_color_code;
            this.results.rand_color = rand_color_code; 
            if (win) {
                this.results.result_txt = 'You Win !!';
            } else {
                this.results.result_txt = 'Equal';
            }

            this.results.pcount += 1;
        
        },
        random_card: function() {
            var max = this.cards.length;
            return Math.floor(Math.random() * max);
        },
        compare_card: function(card_select, card_rand) {
            var result;

            if (card_select == 'red' && card_rand == 'green') {
                result = 1; // win
            }
            else if(card_select == 'green' && card_rand == 'brown') {
                result = 1;
            }
            else if(card_select == 'brown' && card_rand == 'blue') {
                result = 1;
            }
            else if(card_select == 'blue' && card_rand == 'red') {
                result = 1;
            }
            else {
                result = 0;  // equal
            }
            
            return result;

        }
    }
};
</script>

<style>
    .is-select {
        background-color: #2dce89 !important;
    }

    .not-select {
        background-color: #f4f5f7 !important;
    }

    .vs {
        font-size: 50px;
    }

    .card_random {
        border: 5px solid !important;
        border-color: rgb(99, 96, 96) !important;
    }
    
</style>