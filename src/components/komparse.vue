<template>
    <div class="komparse_class">
        <div class="row justify-content-center" id="registerHeading">
            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">Registrieren</h1>
                    <p class="lead" id="description-for-header">Trag hier bitte die Daten für die Komparsenregistrierung
                        ein.
                    </p>
                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-md-4">
                <label for="body_size" class="form-label">Körpergröße in cm</label>
                <input type="number" class="form-control" id="body_size" placeholder="180" required v-model="body_size_input"
                    min="30" max="250">

                <div class="invalid-feedback" id="body_size-feedback">
                    Körpergröße ist erforderlich und muss zwischen 30 und 250 liegen.
                </div>
            </div>

            <div class="col-md-4">
                <label for="cloth_size" class="form-label"> Kleidergröße angeben </label>
                <select class="form-select" aria-label="Default select example" v-model="cloth_size_input" id="cloth_size">
                    <option value selected>Wähle Größe</option>
                    <option value="XS">XS</option>
                    <option value="S">S</option>
                    <option value="M">M</option>
                    <option value="L">L</option>
                    <option value="XL">XL</option>
                    <option value="XXL">XXL</option>
                </select>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h2 class="display-4" id="description-header">Bild hinzufügen</h2>
                    <p class="lead" id="description-for-header">Bitte füg ein Bild von dir hinzu</p>
                </div>

                <div class="form-group" id="pic_uploader1">
                    <div class="input-group">
                        <div class="custom-file">
                            <input type="file" class="form-control" id="input_picture1" aria-describedby="input_picture1">
                            <label class="custom-file-label" for="input_picture1">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png) </span></label>
                            <div id="input_picture1-feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id=img_preview1>
                </div>
            </div>

            <div class="col-lg-4 col-md-6 col-sm-10">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h2 class="display-4" id="description-header">Bild hinzufügen</h2>
                    <p class="lead" id="description-for-header">Bitte füg ein Bild von dir hinzu</p>
                </div>

                <div class="form-group" id="pic_uploader2">
                    <div class="input-group">
                        <div class="custom-file">
                            <input type="file" class="form-control" id="input_picture2" aria-describedby="input_picture2">
                            <label class="custom-file-label" for="input_picture2">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png)</span> </label>
                            <div id="input_picture2-feedback" class="invalid-feedback">
                                Ein Bild ist erforderlich und es werden nur JPEG, JPG und PNG akzeptiert.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" id="img_preview2">
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
let body_size_input = ref(null);
let cloth_size_input = ref(null);
let pic1 = ref(null);
let pic2 = ref(null);

function save_data() {
    
    let obj = {
        "komparse_body_size": body_size_input.value,
        "komparse_cloth_size": cloth_size_input.value,/*
        "lastname": lastname_input.value,
        "email": email_input.value,*/
        

    }

    emit('save-data', obj);
}
</script>