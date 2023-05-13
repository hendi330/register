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

                <div class="form-group" id="pic_uploader1">
                    <div class="input-group">
                        <div class="custom-file">
                            <input type="file" class="form-control" id="driverslicensefront"
                                aria-describedby="driverslicensefront">
                            <label class="custom-file-label" for="driverslicensefront">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png) </span></label>
                            <div id="driverslicensefront-feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id="preview_driverslicensefront">
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

                <div class="form-group" id="pic_uploader2">
                    <div class="input-group">
                        <div class="custom-file">
                            <input type="file" class="form-control" id="driverslicenseback"
                                aria-describedby="driverslicenseback">
                            <label class="custom-file-label" for="driverslicenseback">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png)</span> </label>
                            <div id="driverslicenseback-feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id="preview_driverslicenseback">
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
let driversLincense_back = ref(null);
let driversLincense_front = ref(null);
function save_data() {
    // let tmp_arr = ref({
    //     "umsetzer": {
    //         "driversLincense_back": "german",
    //         "driversLincense_front" :"front"

    //     }
    // });
    
    // emit('save-data', tmp_arr);

    let arr = {
        "umsetzer_driversLincense_back": "german",
        "umsetzer_driversLincense_front" :"front"
    }

    emit('save-data', arr);
}
</script>