<!--<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>-->

<template>
  <header>
  </header>
  <div class="container centerdiv">
    <main>
      <confirmations @all-confirmed="incrementCurrentForm"
        v-if="check_active_form('confirmation') " />
      <jobSelect v-else-if="check_active_form('jobselect')" @toggle-jobselect="toggle_job_activestate"
        @next-form="start_registration" />
      <komparseform v-else-if="check_active_form('komparse')" 
      @save-data="add_data_to_array"/>
      <cookform v-else-if="check_active_form('cook')" 
      @save-data="add_data_to_array"/>
      <umsetzerform v-else-if="check_active_form('umsetzer')" 
      @save-data="add_data_to_array"/>
      <serviceform v-else-if="check_active_form('service') " 
      @save-data="add_data_to_array"/>
      <personalInfo v-else-if="check_active_form('personalinfo')" 
      @save-data="add_data_to_array" />
      <location v-else-if="check_active_form('location')" 
      @save-data="registration_complete" />

      <!--<personalInfo v-if="forms[current_form]" main_heading="Registrieren" sub_heading ="Um dich zu registrieren musst du alle felder ausfüllen."/> -->


      
    </main>
  </div>
</template>
<script setup>

import jobSelect from './components/jobselect.vue'
import personalInfo from './components/personalinfo.vue'
import location from './components/location.vue'
import confirmations from './components/confirmations.vue'
import komparseform from './components/komparse.vue'
import cookform from './components/cook.vue'
import umsetzerform from './components/umsetzer.vue'
import serviceform from './components/service.vue'
//wie viele forms, welche forms. 
import { ref, toRaw, unref } from 'vue';
let registration_infos = ref([]);

let current_form = ref(0);
console.log(current_form);
let active_job = ref("confirmation");
let forms = ref({
  "confirmation": { "active": true,"order": 0 },
  "jobselect": { "active": true, "order": 1 },
  "komparse": { "active": false, "order": 2 },
  "cook": { "active": false, "order": 3 },
  "umsetzer": { "active": false, "order": 4 },
  "service": { "active": false, "order": 5 },
  "personalinfo": { "active": true, "order": 6 },
  "location": { "active": true, "order": 7 },
});

let max_forms = ref(4);


function toggle_job_activestate(job) {
  forms.value[job].active = !forms.value[job].active;
  

}
const incrementCurrentForm = () => {
  //immer wenn  eine neue form angezeigt werden soll
  current_form.value = (current_form.value + 1);
  forms.value[active_job.value].active = !forms.value[active_job.value].active

};
function start_registration() {
  incrementCurrentForm();
  let tmp_arr = [];
  tmp_arr.push({"cook":forms.value.cook.active});
  tmp_arr.push({"komparse":forms.value.komparse.active});
  tmp_arr.push({"umsetzer":forms.value.umsetzer.active});
  tmp_arr.push({"service":forms.value.service.active});
  registration_infos.value.push(tmp_arr.value);

}
console.log(forms.value["komparse"]);
function check_active_form(job) {
  //check first if form is even active
  if (forms.value[job].active) {
    /*if form is active check if currentform equals the index (order)
    if (forms.value[job].order == current_form.value) {

      console.log("return true");
      return true;
    }*/
    active_job.value = job;
    return true;
   
    
  }
  //if not 
  else {
    return false;
  }
}


function add_data_to_array(data){
  registration_infos.value.push(data);
  incrementCurrentForm();
}

function registration_complete(data){
  registration_infos.value.push(data);
  console.log(registration_infos);
  // retrieve information from proxy object
  let reg = toRaw(registration_infos.value);
  
  // merge the properties from all registration_info objects into one
  let fullobj = {};
  reg.forEach(element => {
    // do encodeURIComponent() for every element in the object
    Object.keys(element).forEach(key => {
      element[key] = encodeURIComponent(element[key]);
    });
    fullobj = {...fullobj, ...element};
  });

  console.log("fullobj", fullobj); 
  send_data(fullobj);
}

function send_data(obj) {
  // for files, convert them to base64 images and send them inside the body, seperate multiple files with linebreaks
  // make sure to escape equal signs following the base64 string with %3D
  let body = "";
  let files = [1];
  files.forEach(file => {
    let key = "umsetzer_driversLincense_back"
    let filename = "red dot.png";
    let type = "image/png";
    let base64content = "iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVQI12P4//8/w38GIAXDIBKE0DHxgljNBAAO9TXL0Y4OHwAAAABJRU5ErkJggg=="
    
    body += `key=${encodeURIComponent(key)}&filename=${encodeURIComponent(filename)}&content=data:${encodeURIComponent(type)};base64, ${encodeURIComponent(base64content)}\n`;
  })
  
  
  fetch("http://localhost:5001/contact/", {
    method: "POST",
    body: body,
    headers: obj,
  })
  .then(response => response.json())
  .then(data => {
    console.log("returned data", data);
  })
  .catch(error => {
    console.error(error);
  });
}


</script>
<!--
<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
-->