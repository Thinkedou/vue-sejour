<script setup>
import {ref} from 'vue'

const rawRecap = localStorage.getItem("sejourRecap");
const recap = ref({})
if(rawRecap){
  recap.value = JSON.parse(rawRecap)
}


</script>

<template>

<div class="container d-flex justify-content-center">
  <div class="card" style="width: 18rem;">
    <img src="@/assets/img/default.jpg" class="card-img-top" alt="default">
    <div class="card-body">
      <h5 class="card-title">Votre Récap {{recap.totalPrice}}</h5>
      <p class="card-text">Nous vous souhaitons un bon séjour <strong>{{recap.lastName}}</strong> {{recap.firstName}} </p>
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">Hébergement:  <strong>Tentes</strong></li>
      <li class="list-group-item">Kayak ⛴ & Draps</li>
      <li class="list-group-item"><strong>Options déjeuner</strong></li>
    </ul>
    <div class="card-body">
        <button id="submitButton" type="button" class="btn btn-lg btn-block btn-primary">Confirmer</button>
    </div>
  </div>
    
</div>
</template>
