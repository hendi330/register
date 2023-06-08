<template>
    <div class="umsetzer_class">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Reich hier bitte deinen Führerschein (C/C1) ein.</p>
                </div>
            </div>
        </div>


        <div class="row justify-content-center">
            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h2 class="display-4" id="description-header">Bild hinzufügen - Führerschein
                        <small>(Vorderseite)</small>
                    </h2>
                    <p class="lead" id="description-for-header">Bitte füg ein Bild von der <b>Führerschein
                            Vorderseite</b> hinzu
                    </p>
                </div>

                <div class="form-group" id="front_license_uploader">
                    <div class="input-group">
                        <div class="custom-file">
                            <input @change="save_license('front', $event)" type="file" class="form-control"
                                id="front_license_input" aria-describedby="front_license">
                            <label class="custom-file-label" for="front_license">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png) </span></label>
                            <div id="front_license-feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id="front_license_preview">
                </div>
            </div>

            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h2 class="display-4" id="description-header">Bild hinzufügen - Führerschein
                        <small>(Rückseite)</small>
                    </h2>
                    <p class="lead" id="description-for-header">Bitte füg ein Bild von der<b>Führerschein Rückseite</b>
                        hinzu</p>
                </div>

                <div class="form-group" id="back_license_uploader">
                    <div class="input-group">
                        <div class="custom-file">
                            <input @change="save_license('back', $event)" type="file" class="form-control"
                                id="back_license_input" aria-describedby="back_license">
                            <label class="custom-file-label" for="back_license">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png)</span> </label>
                            <div id="back_license_feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id="back_license_preview">
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
let driversLicense_back = ref(null);
let driversLicense_front = ref(null);
function save_data() {
    // let tmp_arr = ref({
    //     "umsetzer": {
    //         "driversLincense_back": "german",
    //         "driversLincense_front" :"front"

    //     }
    // });

    // emit('save-data', tmp_arr);

    let arr = {
        umsetzer_driversLicense_back: driversLicense_back.value,
        umsetzer_driversLicense_front: driversLicense_front.value
    }

    emit('save-data', arr);
}

function save_license(what, e) {
    console.log(e);

    // let file = event.target.files[0];
    // let reader = new FileReader();
    // reader.readAsDataURL(file);
    // reader.onload = function () {
    //     driversLicense_back.value = reader.result;
    //     document.getElementById("preview_driverslicenseback").src = driversLicense_back.value;
    // };
    // reader.onerror = function (error) {
    //     console.log('Error: ', error);
    // };
    let feedback;
    let input;
    let preview;
    if (what == 'back') {
        feedback = document.getElementById("back_license_feedback");
        input = document.getElementById("back_license_input");
        preview = document.getElementById("back_license_preview");
    }
    else if (what == 'front') {
        feedback = document.getElementById("front_license-feedback");
        input = document.getElementById("front_license_input");
        preview = document.getElementById("front_license_preview");
    }

    if (e.target.files[0].type != 'image/jpeg' && e.target.files[0].type != 'image/png') {
        if (!(input.classList.contains('is-invalid'))) {
            input.classList.add('is-invalid');
            feedback.style.display = 'block';
        }
    }
    else {
        if (input.classList.contains('is-invalid')) {
            input.classList.remove('is-invalid');
            feedback.style.display = 'none';
        }
        let reader = new FileReader();
        reader.readAsDataURL(e.target.files[0]);
        reader.onload = function () {

            //save base64 to variable
            console.log(reader.result);
            //string starts with: data:image/jpeg;base64, - CUT IT OUT
            let tmp = reader.result.split(',');
            if (what == 'front') {
                driversLicense_front.value = tmp[1];
                preview.src = reader.result;

            }
            else if (what == 'back') {
                driversLicense_back.value = tmp[1];
                preview.src = reader.result;

            }

        }

    }
}
</script>