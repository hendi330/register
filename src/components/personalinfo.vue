<template >
    <div class="personalinfo_class">
        <div class="row justify-content-center">

            <div class="col-lg-9 col-md-10 col-sm-11">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h1 class="display-4" id="description-header">{{ main_heading }}</h1>
                    <p class="lead" id="description-for-header">{{ sub_heading }}</p>
                </div>
                <!--<form class="needs-validation" novalidate>-->
                <div class="row justify-content-center">

                    <div class="col-12 col-sm-2">
                        <label for="gender" class="form-label"> Anrede </label>
                        <select v-model="gender_input" class="form-select" aria-label="Default select example" id="gender">
                            <option value="" selected>Wähle Anrede</option>
                            <option value="male">Herr</option>
                            <option value="female">Frau</option>
                        </select>
                        <div id="gender-feedback" class="invalid-feedback">
                            Gib bitte eine Anrede an.
                        </div>
                    </div>
                    <div class="col-12 col-sm-5">
                        <label for="firstName" class="form-label">Vorname</label>
                        <input v-model="firstname_input" type="text" class="form-control" id="firstName" required>
                        <div class="invalid-feedback" id="firstName-feedback">
                            Ein Vorname ist erforderlich.
                        </div>
                    </div>

                    <div class="col-12 col-sm-5">
                        <label for="lastName" class="form-label">Nachname</label>
                        <input v-model="lastname_input" type="text" class="form-control" id="lastName" required>
                        <div class="invalid-feedback" id="lastName-feedback">
                            Ein Nachname ist erforderlich.
                        </div>
                    </div>


                    <div class="col-12" id="margin_top_20">
                        <label for="email" class="form-label">Email</label>
                        <input type="email" class="form-control" id="email" v-model="email_input" required>
                        <div class="invalid-feedback" id="email-feedback">
                            Eine Email Adresse ist erforderlich
                        </div>
                    </div>

                    <div class="col-12" id="margin_top_20">
                        <label for="phonenumber" class="form-label">Telefonnummer<span
                                class="text-muted">(Handynummer)</span></label>
                        <input v-model="phonenumber_input" type="number" class="form-control" id="phonenumber" required>
                        <div class="invalid-feedback" id="phonenumber-feedback">
                            Eine Telefonnummer ist erforderlich
                        </div>
                    </div>



                    <div class="col-6 margin_topbot_20">
                        <label for="birthdate" class="form-label">Geburtsjahr <span
                                class="text-muted">(Optional)</span></label>
                        <input v-model="birthdate_input" type="date" class="form-control" id="birthdate"
                            placeholder="01.01.1900">
                        <div class="invalid-feedback" id="birthdate-feedback">
                            Bitte geben Sie ein Geburtsjahr ein.
                        </div>
                    </div>
                    <div class="col-6 margin_topbot_20">
                        <label for="drivers_license" class="form-label">
                            Führerschein
                        </label>
                        <select v-model="drivers_license_input" class="form-select" aria-label="Default select example"
                            name="drivers_license" id="drivers_license">
                            <option value="Nein" selected>Nein</option>
                            <option value="Ja">Ja</option>
                        </select>
                    </div>
                </div>




                <!-- </form>-->



            </div>
            <div class="col-lg-4 col-md-6 col-sm-9" id="pic-uploader">
                <div class="pricing-header pt-md-5 mx-auto text-center">
                    <h2 class="display-4" id="description-header">Bild hinzufügen</h2>
                    <p class="lead" id="description-for-header">Bitte füg ein Bild von dir hinzu</p>
                </div>

                <div class="form-group" id="pic_uploader">
                    <div class="input-group">
                        <div class="custom-file">
                            <input type="file" class="form-control" id="input_picture" aria-describedby="input_picture">
                            <label class="custom-file-label" for="input_picture">Wähle ein Bild aus <span
                                    class="text-muted">(akzeptierte Formate: jpg, jpeg, png) </span></label>
                            <div class="invalid-feedback" id="input_picture-feedback">
                                Nur Bilder sind erlaubt, erlaubt Formate: JPEG, JPN, PNG.
                            </div>

                        </div>
                    </div>

                </div>
                <div class="row">
                    <img src="#" class="img-fluid" id="img_preview">
                </div>
            </div>
        </div>
        <div class="row justify-content-center margin-bottom-5 mt-3">
            <div class="col-10">
                <div class="row mt-20 mb-20">
                    <div class="btn-group">
                        <button type="submit" class="btn btn-danger">Zurück zum Anfang</button>

                        <button class="btn btn-primary" type="button" @click="save_data()" :disabled="!inputs_checked">Weiter</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref, computed, onUpdated } from 'vue';
import { defineEmits } from 'vue';
const emit = defineEmits(['save-data']);

const props = {
    main_heading: {
        type: String,
        default: "Registrieren"
    },
    sub_heading: {
        type: String,
        default: "Bitte Fülle alle leeren Felder aus."
    }
}
let gender_input = ref(null);
let firstname_input = ref(null);
let lastname_input = ref(null);
let email_input = ref(null);
let phonenumber_input = ref(null);
let birthdate_input = ref(null);
let drivers_license_input = ref(null);

let inputs_checked = ref(false);
function check_inputs(){

}
function save_data() {
    // let tmp_arr = ref({
    //     "personalinfo": {
    //         "gender": gender_input.value,
    //         "firstname": firstname_input.value,
    //         "lastname": lastname_input.value,
    //         "email": email_input.value,
    //         "phonenumber": phonenumber_input.value,
    //         "birthdate": birthdate_input.value,
    //         "drivers_license": drivers_license_input.value,

    //     }
    // });
    
    // emit('save-data', tmp_arr);

    let arr = {
        "personalinfo_gender": gender_input.value,
        "personalinfo_firstname": firstname_input.value,
        "personalinfo_lastname": lastname_input.value,
        "personalinfo_email": email_input.value,
        "personalinfo_phonenumber": phonenumber_input.value,
        "personalinfo_birthdate": birthdate_input.value,
        "personalinfo_drivers_license": drivers_license_input.value,
    }

    emit('save-data', arr);
}
onUpdated(() => {
    if(gender_input.value != "" && gender_input.value != null && firstname_input.value != "" && firstname_input.value != null && lastname_input.value != "" && lastname_input.value != null && email_input.value != "" && email_input.value != null && phonenumber_input.value != "" && phonenumber_input.value != null && birthdate_input.value != "" && birthdate_input.value != null /*&& drivers_license_input.value != "" && drivers_license_input.value != null*/){
        console.log(gender_input.value);
        inputs_checked.value = true;
    }
    else{
        inputs_checked.value = false;
    }
});

</script>