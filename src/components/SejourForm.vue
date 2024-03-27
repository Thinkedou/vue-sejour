<script setup>
import {ref} from 'vue'

const emit = defineEmits(['onFormChange'])


const firstName = ref('')
const lastName  = ref('')
const typeHebergement = ref('default')
const sejourOptions = ref([])
const ptiDej = ref('false')
const prixTotal = ref(0)

const formErrors = ref([])

const hebergementPrice = {
  default:0,
  tente:30,
  toile:50,
  pierre:100
}

const okHandler = ()=>{
      const recapCommand = {}
}

const updateFormHandler = ()=>{
  // première étape: calcul de l'hebergement de base
  prixTotal.value = 0
  formErrors.value.length = 0
  prixTotal.value = hebergementPrice[typeHebergement.value]


  if(typeHebergement.value=='default'){
    formErrors.value.push('merci de séléctionner un type d\'hebergement')
  }

  if(sejourOptions.value.length>0){
      if(sejourOptions.value.includes('kayak')){
        prixTotal.value+=30
      }
      if(sejourOptions.value.includes('draps')){
        prixTotal.value+=5
      }
  }

  if(ptiDej.value=="true"){
    prixTotal.value+=10
  }
  console.warn('PRIX TOTAL::::', prixTotal.value )
  const toSend = {
    hebergement:typeHebergement.value,
    price:prixTotal.value
  }
  emit('onFormChange',toSend)
}




</script>

<template>
<div class="col-8">
            <div class="card mb-4 shadow-sm">
              <div class="card-header">
                <h4 class="my-0 font-weight-normal">Configurer votre séjour</h4>
              </div>
              <div class="card-body">

                <div class="row mb-2">
                  <div class="col">
                    <input type="text" class="form-control" placeholder="Nom" v-model="lastName">
                  </div>
                  <div class="col">
                    <input type="text" class="form-control" placeholder="Prénom" v-model="firstName">
                  </div>
                </div>



                <!-- Select   -->
                <label for="type">Type d'hebergement :  </label>
                <select 
                  @change="updateFormHandler"
                  class="custom-select d-btypelock w-100" v-model="typeHebergement">
                  <option value="default">Choisissez...</option>
                  <option value="tente">Emplacement Tentes</option>
                  <option value="toile">Toile</option>
                  <option value="pierre">Pierre</option>
                </select>

                <hr class="mb-4">
                <!-- Checkboxes button  -->
                <h4 class="my-2">Les options de séjour </h4>
                <span>{{sejourOptions}}</span>
                <div class="custom-control custom-checkbox">
                  <input v-model="sejourOptions" @change="updateFormHandler" type="checkbox" class="custom-control-input" name="optionsSejour" value="kayak" id="ok-kayak">
                  <label class="custom-control-label" for="ok-kayak">Location Kayak (+30€)</label>
                </div>
                <div class="custom-control custom-checkbox">
                  <input v-model="sejourOptions" @change="updateFormHandler" type="checkbox" class="custom-control-input" name="optionsSejour" value="draps" id="ok-draps">
                  <label class="custom-control-label" for="ok-draps">Draps (+5€) </label>
                </div>
                <h4 class="mt-3">Petit Déjeuner</h4>

                    <div class="d-block my-3">
                      <div class="custom-control custom-radio">
                        <input @change="updateFormHandler" id="ouiPetitDej" value="true" v-model="ptiDej" name="petitDej" type="radio" class="custom-control-input" checked >
                        <label class="custom-control-label" for="ouiPetitDej">Oui (+10€)</label>
                      </div>
                      <div class="custom-control custom-radio">
                        <input @change="updateFormHandler" id="nonPetitDej"  value="false" v-model="ptiDej" name="petitDej" type="radio" class="custom-control-input" >
                        <label class="custom-control-label" for="nonPetitDej">Non</label>
                      </div>
                </div>
                <div v-if="formErrors.length>0" class="alert alert-warning" role="alert">
                  Erreur, merci de séléctionner un hébergement
                </div>
                <div class='mt-2'>
                    <button @click="okHandler" type="button" class="btn btn-lg btn-block btn-primary">Ok</button>
                </div>

              </div>
            </div>
        </div>
</template>