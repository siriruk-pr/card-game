<template>
    <!-- Modals -->
    <div class="row">
        <div class="col-md-4">
            
            <modal :show.sync="modals.modal1">
                <h6 slot="header" class="modal-title" id="modal-title-default">Battle Result</h6>
                    <div class="col-lg-12 mt-3">
                        <div class="row row-grid justify-content-center">
                            <div class="col-lg-6 col-md-6 col-sm-6 text-center">
                                <div>
                                    <card class="border-card" hover shadow body-classes="py-5" v-bind:style="{ 'background-color': sel_color }">
                                        <h6 class="text-uppercase display-4">You</h6>
                                    </card>
                                </div>
                            </div>
                            <div class="col-lg-6 col-md-6 col-sm-6 text-center">
                                <div>
                                    <card class="card_random" hover shadow body-classes="py-5" v-bind:style="{ 'background-color': rand_color }">
                                        <h6 class="text-uppercase display-4">Random</h6>
                                    </card>
                                </div>
                            </div>
                            <div class="col-lg-12 col-md-6 col-sm-6 text-center mt-5">
                                <div class="result_txt">
                                    <h4>{{ result_txt }}</h4>
                                </div>
                            </div>
                        </div>
                    </div>
                <template slot="footer">
                    <base-button type="link" class="ml-auto" @click="modals.modal1 = false">Close
                    </base-button>
                </template>
            </modal>
        </div>
    </div>
</template>
<script>
import Modal from "@/components/Modal.vue";
export default {
    components: {
        Modal
    },
    props: ['sel_color', 'rand_color', 'result_txt', 'pcount'],
    data() {
        return {
            modals: {
                modal1: false,
            }
        }
    },
    watch: { 
      	pcount: function(newVal, oldVal) { // watch it
            if (newVal > 0) {
                this.modals.modal1 = true;
            }
        }
    }
};
</script>
<style>
    .result_txt {
        font-weight: bold;
    }
</style>
