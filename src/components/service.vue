<template>
    <div class="service_class">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Das ist das Anmeldeformular für Streetkitchen. Bitte
                        Füllen
                        Sie
                        alle nötigen Felder aus. </p>
                </div>

            </div>
        </div>
        <div class="row justify-content-center" id="language-row">
            <div class="col-11">

                <p>Trage Sprachen ein, die du sprechen kannst.</p>

                <div class="input-group mb-3">
                    <input id="language_inputfield" type="text" class="copy-form-control-File" placeholder="Englisch"
                        aria-label="Recipient's username" aria-describedby="button-addon2">
                    <button class="btn btn-outline-secondary" onclick="add_language()" type="button" id="button-addon2">Füg
                        eine
                        Sprache hinzu</button>
                    <div id="language-feedback" class="invalid-feedback">
                        Sicher, dass du keine Sprache angeben willst?
                    </div>
                </div>

            </div>

        </div>
        <div class="row justify-content-center margin-bottom-5 mt-3">
            <div class="col-10">
                <div class="row mt-20 mb-20">
                    <div class="btn-group">
                        <button @click="back_to_start()" class="btn btn-danger">Zurück zum Anfang</button>

                        <button class="btn btn-primary" type="button" @click="save_data()">Weiter</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { defineEmits } from 'vue';
const emit = defineEmits(['save-data', 'back-to-start']);
let languages_input = ref(null);
function back_to_start() {
    emit('back-to-start');
}
function save_data() {
    // let tmp_arr = ref({
    //     "service": {
    //         "languages": "german",
            

    //     }
    // });
    
    
    // emit('save-data', tmp_arr);

    let arr = {
        service_languages: "german",
        service: true,
    }

    emit('save-data', arr);
}
</script>