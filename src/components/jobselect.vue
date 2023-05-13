<template>
    <div class="jobselect_class">
    <div class="row justify-content-center">
        <div class="col-md-6 col-12">
            <div class="card-deck mb-3 text-center " id="cook-card">
                <div class="card mb-4 box-shadow customcard" id="cook-card-col">
                    <div class="card-header" id="cook-cardheader">
                        <h4 class="my-0 font-weight-normal" id="form-header">Koch/Köchin</h4>
                    </div>
                    <div class="card-body" id="form-content">
                        <h5 class="card-title pricing-card-title text-center"><small
                                class="text-muted">Anforderungen</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Nachweis Kocherfahrung</li>
                            <li>Gute Sprachkenntnisse in Englisch oder Deutsch</li>
                            
                            <br><br>

                        </ul>
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Was wir bieten</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Flexible Arbeitszeiten</li>
                            <li>Wechselnde oder feste Arbeitsplätze</li>

                        </ul>
                        <button @click="toggle_jobselect('cook')" type="button" id="select-btn-cook"
                            class="btn btn-lg btn-block btn-outline-primary ">Der Auswahl
                            hinzufügen</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="col-md-6 col-12">
            <div class="card-deck mb-3 text-center " id="service-card">
                <div class="card mb-4 box-shadow customcard" id="service-card-col">
                    <div class="card-header" id="service-cardheader">
                        <h4 class="my-0 font-weight-normal" id="form-header">Service Kraft</h4>
                    </div>
                    <div class="card-body text-left" id="form-content">
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Anforderungen</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Freundlicher Umgang mit Gästen</li>
                            <li>Gute Sprachkenntnisse in Deutsch oder Englisch</li>
                            <li>Arbeiten in Küche & Buffet</li>
                            <li>Gästeservice, Buffetservice</li>
                        </ul>
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Was wir bieten</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Flexible Arbeitszeiten</li>
                            <li>Wechselnde Arbeitsplätze</li>

                        </ul>
                        <button @click="toggle_jobselect('service')" type="button" id="select-btn-service"
                            class="btn btn-lg btn-block btn-outline-primary ">Der Auswahl
                            hinzufügen</button>
                    </div>
                </div>
            </div>
        </div>


        <div class="col-md-6 col-12">
            <div class="card-deck mb-3 text-center" id="komparse-card">
                <div class="card mb-4 box-shadow customcard" id="komparse-card-col">
                    <div class="card-header" id="komparse-cardheader">
                        <h4 class="my-0 font-weight-normal green" id="form-header">Als Komparse</h4>
                    </div>
                    <div class="card-body" id="form-content">
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Anforderungen</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Jeder der interasse an Filmarbeiten hat.</li>

                        </ul>
                        <h5 class="card-title pricing-card-title"><small class="text-muted">ZU BEACHTEN</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Arbeitszeiten sehr Flexibel und <b>nicht</b> kontinuierlich</li>
                            <br>

                        </ul>
                        <button type="button" @click="toggle_jobselect('komparse')" data-bs-toggle="button"
                            id="select-btn-komparse" class="btn btn-lg btn-block btn-outline-primary ">Der
                            Auswahl hinzufügen</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-md-6 col-12">
            <div class="card-deck mb-3 text-center" id="umsetzer-card">
                <div class="card mb-4 box-shadow customcard" id="umsetzer-card-col">
                    <div class="card-header" id="umsetzer-cardheader">
                        <h4 class="my-0 font-weight-normal" id="form-header">Umsetzer/-in</h4>
                    </div>
                    <div class="card-body" id="form-content">
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Anforderungen</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>LKW Führerschein (C/C1)</li>


                        </ul>
                        <h5 class="card-title pricing-card-title"><small class="text-muted">Was wir bieten</small></h5>
                        <ul class="list-unstyled mt-3 mb-4 list text-start">
                            <li>Flexible Arbeitszeiten</li>
                            <li>Wechselnde Arbeitsplätze</li>

                        </ul>
                        <button type="button" id="select-btn-umsetzer" @click="toggle_jobselect('umsetzer')"
                            class="btn btn-lg btn-block btn-outline-primary">Der Auswahl
                            hinzufügen</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-10 mb-3">
            <div class="row justify-content-end">
                <button type="button" id="continue-btn" @click="next_form"
                    :class="['btn', 'btn-lg', 'btn-block', 'btn-outline-primary']">Weiter</button>
            </div>
            <div id="pic1-feedback" class="invalid-feedback">
                Bitte wähle mindestens eines der vier verschiedenen Angebote aus.
            </div>
        </div>



    </div>
</div>
</template>
<script setup>
import { ref, computed } from 'vue';
import { defineEmits } from 'vue';

const emit = defineEmits(['toggle-jobselect' , 'next-form']);
function toggle_jobselect(job){

    emit('toggle-jobselect', job);
    document.getElementById(job +"-card-col").classList.toggle("active");
}

function next_form(){
    emit('next-form');
}
</script>
<!-- <script>
export default {
    data() {
        return {
            isChecked1: false,
            isChecked2: false,
            isChecked3: false,
        };
    },
    methods: {
        toggle_jobselect(job, toggle) {
            this.$parent.toggle_job_activestate(job);
            toggle.classList.toggle("active");

        }
    },
    
}
</script> -->