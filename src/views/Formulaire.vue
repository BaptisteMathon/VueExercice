<script setup lang="ts">
import {reactive, ref} from 'vue'
import type {Formulaire} from '@/models/formModel'

const form:Formulaire = reactive({
  nom: '',
  prenoms: '',
  email: '',
  sexe: '',
  adresse: '',
  codepostal: '',
  ville: '',
  nominstitut: ''
})

const submitted = ref(false)

const missing = ref<string[]>([])

const onSubmit = () => {
  missing.value = []
  switch(true){
    case !form.nom:
      missing.value.push("Champ Nom incorrect");
      break;
    case !form.prenoms:
      missing.value.push("Champ Prénoms incorrect");
      break;
    case !form.email:
      missing.value.push("Champ Email incorrect");
      break;
    case !form.sexe:
      missing.value.push("Champ Sexe incorrect");
      break;
    case !form.adresse:
      missing.value.push("Champ Adresse incorrect");
      break;
    case !form.codepostal:
      missing.value.push("Champ Code Postal incorrect");
      break;
    case !form.ville:
      missing.value.push("Champ Ville incorrect");
      break;
    case !form.nominstitut:
      missing.value.push("Champ Nom de l'institut incorrect");
      break;
    default:
      submitted.value = true
  }
}
</script>

<template>
  <div>
    <div v-if="missing.length > 0">
      <p id="error" v-for="error in missing">{{ error }}</p>
    </div>
    <h1>Forumlaire d'inscription</h1>
    <form @submit.prevent="onSubmit">
      <div>
        <label for="name">Nom: </label>
        <input type="text" id="nom" v-model="form.nom">
      </div>

      <div>
        <label for="prenoms">Prénoms: </label>
        <input type="text" id="prenoms" v-model="form.prenoms">
      </div>

      <div>
        <label for="email">Email: </label>
        <input type="email" id="email" v-model="form.email">
      </div>

      <div>
        <label for="sexe">Sexe: </label>
        <input type="radio" id="homme" value="homme" v-model="form.sexe">
        <label for="homme">Homme</label>
        <input type="radio" id="femme" value="Femme" v-model="form.sexe" />
        <label for="femme">Femme</label>
      </div>

      <div>
        <label for="adresse">Adresse: </label>
        <input type="text" id="adresse" v-model="form.adresse" />
      </div>

      <div>
        <label for="codepostal">Code Postal: </label>
        <input type="text" id="codepostal" v-model="form.codepostal" />
      </div>

      <div>
        <label for="ville">Ville:</label>
        <input type="text" id="ville" v-model="form.ville" />
      </div>

      <div>
        <label for="nominstitut">Nom de l'institut:</label>
        <input type="text" id="nominstitut" v-model="form.nominstitut" />
      </div>

      <button type="submit">Valider</button>
    </form>
  </div>

  <div v-if="submitted">
    <h2>Récapitulatif informations saisies:</h2>
    <p>Nom: {{ form.nom }}</p>
    <p>Prénoms: {{ form.prenoms }}</p>
    <p>Email: {{ form.email }}</p>
    <p>Sexe: {{ form.sexe }}</p>
    <p>Adrese: {{ form.adresse }}</p>
    <p>Code Postal: {{ form.codepostal }}</p>
    <p>Vile: {{ form.ville }}</p>
    <p>Nom de l'institut: {{ form.nominstitut }}</p>
  </div>
</template>

<style>
  #error{
    color: red;
  }
</style>
