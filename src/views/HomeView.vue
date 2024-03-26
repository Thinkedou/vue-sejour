<script setup>
import {ref} from 'vue'
import SejourForm from '../components/SejourForm.vue'

const typeHebergement = ref('default')

const formChangeHandler = (data)=>{
  console.warn('Event depuis le formulaire!!',data)
  typeHebergement.value = data
}

</script>

<template>

<div class="container">

    <div class="row" >
        <SejourForm 
          @onFormChange="formChangeHandler"
        />
        <div class="col-4">

            <div class="card" style="width: 18rem;">
              <img :src="`./src/assets/img/${typeHebergement}.jpg`" class="card-img-top" alt="">
            <div class="card-body">
              <h6 class="card-title text-center">150€</h6>
            </div>
          </div>

        </div>
    </div>
</div>
</template>
