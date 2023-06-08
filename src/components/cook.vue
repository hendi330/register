<template>
    <div class="cook">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Trag hier bitte deinen Kocherfahrungsnachweis ein.</p>
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
                        eine Sprache hinzu</button>
                    <div id="language-feedback" class="invalid-feedback">
                        Sicher, dass du keine Sprache angeben willst?
                    </div>
                </div>

            </div>

        </div>
        <div class="row justify-content-center">
            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h4 class="display-6" id="description-header">Dokument hinzufügen</h4>
                    <p> <small>(Lebenslauf, Ausbildungsnachweis,...)</small></p>
                    <p class="lead" id="description-for-header">Bitte lade ein PDF hoch.</p>
                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-11">
                <div class="form-group" id="pic_uploader1">
                    <div class="input-group">
                        <div class="custom-file">
                            <input @change="save_pdf($event, 'req')" type="file" class="form-control" id="nachweis" aria-describedby="nachweis">
                            <label class="custom-file-label" for="nachweis">PDF auswählen <span
                                    class="text-muted">(akzeptierte
                                    Formate: pdf) </span></label>
                            <div id="nachweis-feedback" class="invalid-feedback">
                                Bitte lade die Datei als PDF hoch.
                            </div>

                        </div>
                    </div>

                </div>
            </div>

            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h3 class="display-6" id="description-header">Zusätzliches Dokument</h3>
                    <p> <small>(optional)</small></p>
                    <p class="lead" id="description-for-header">Lade noch ein zusätzliches Dokument hoch.</p>
                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-11">
                <div class="form-group" id="pic_uploader2">
                    <div class="input-group">
                        <div class="custom-file">
                            <input @change="save_pdf($event, 'opt')" type="file" class="form-control" id="nachweis_optional"
                                aria-describedby="nachweis_optional">
                            <label class="custom-file-label" for="nachweis_optional">PDF auswählen <span
                                    class="text-muted">(akzeptierte Formate: pdf)</span> </label>
                            <div id="nachweis_optional-feedback" class="invalid-feedback">
                                Bitte lade die Datei als PDF hoch.
                            </div>

                        </div>
                    </div>

                </div>
            </div>

        </div>
        <div class="row justify-content-center margin-bottom-5 mt-3">
            <div class="col-10">
                <div class="row mt-20 mb-20">
                    <div class="btn-group">
                        <button type="submit" class="btn btn-danger">Zurück zum Anfang</button>

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
const emit = defineEmits(['save-data']);
let language_input = ref(null);
let file1_input = ref(null);
let file2_input = ref(null);
function save_data() {

    let arr = {
        cook_languages: "german",
        cook_confirmation_pdf_req: file1_input.value,
        cook_confirmation_pdf_opt: file2_input.value,

    }

    emit('save-data', arr);
}
function save_pdf(e, type){
    console.log(e.target.files[0].type);
    let feedback;
    let input;
    if(type == 'req'){
        feedback = document.getElementById('nachweis-feedback');
        input = document.getElementById('nachweis');
    }
    else{
        feedback = document.getElementById('nachweis_optional-feedback');
        input = document.getElementById('nachweis_optional');
    }

    if (e.target.files[0].type != 'application/pdf') {
        if(!(input.classList.contains('is-invalid'))){
            input.classList.add('is-invalid');
            feedback.style.display = 'block';
        }
    }
    else{
        if(input.classList.contains('is-invalid')){
            input.classList.remove('is-invalid');
            feedback.style.display = 'none';
        }
        console.log(e.target.files[0]);
        let reader = new FileReader();
        reader.readAsDataURL(e.target.files[0]);
        reader.onload = function () {
        if(type == 'req'){
            file1_input.value = reader.result;
        }
        else{
            file2_input.value = reader.result;
        }
    }
    }
    
    
}
</script>