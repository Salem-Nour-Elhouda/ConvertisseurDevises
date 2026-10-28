<script setup>
import { ref, watch } from 'vue'
import { devises, taux } from '../data/taux.js'

// Variables de base
const montant = ref('0')
const deviseSource = ref('USD')
const deviseCible = ref('EUR')
const resultat = ref('')
const erreurMessage = ref(false)

// Fonction standard pour gerer le clavier numerique
function appuyer(touche) {
  erreurMessage.value = false
  
  if (touche == 'C') {
    montant.value = '0'
    resultat.value = ''
  } 
  else {
    // Verification pour ne pas mettre deux points decimals
    if (touche == '.' && montant.value.includes('.')) {
      return
    }
    // Limitation de la longueur a 10 caracteres
    if (montant.value.length >= 10) 
    {
      return
    }
    // Remplacement du 0 initial

    if (montant.value == '0' && touche !== '.')
     {
      montant.value = touche
    } 
    else 
    {
      montant.value += touche
    }
  }
}

// Fonction de conversion
function convertir() 
{
  if (montant.value == '0' || montant.value == '') 
  {
    erreurMessage.value = true
    return
  }
  erreurMessage.value = false
  
  // Calcul l'euro 
  const m = parseFloat(montant.value)
  const montantEur = m / taux[deviseSource.value]
  const res = montantEur * taux[deviseCible.value]
  
  // Arrondi a 2 decimales
  resultat.value = res.toFixed(2)
}

// Fonction pour inverser les devises
function inverser() 
{
  const temp = deviseSource.value
  deviseSource.value = deviseCible.value
  deviseCible.value = temp
  
  if (resultat.value != '') {
    convertir()
  }
}

/* quest facultatif
Conversion automatique lors des changements */

watch([montant, deviseSource, deviseCible], function() {
  if (montant.value != '0' && montant.value != '') {
    convertir()
  }
})
</script>

<template>
  <div class="card">
    <h1>Currency Converter</h1>
    
    <div class="top">
      <div class="row">

        <select v-model="deviseSource"> 
          <option v-for="d in devises" :key="d" :value="d">{{ d }}</option>
        </select>

         <!--la saisie dans div c est pas dans input-->
        <div class="val">{{ montant }}</div>

      </div>
      
      <button class="btn-inv" @click="inverser">⇄</button>
      
      <div class="row">
        <select v-model="deviseCible">
          <option v-for="d in devises" :key="d" :value="d">{{ d }}</option>
        </select>
        <div class="val">{{ resultat }}</div>
      </div>
      
      <button class="btn-conv" @click="convertir">CONVERTIR</button>
      <p v-if="erreurMessage" class="err">Veuillez saisir un montant</p>
    </div>
    
    <div class="grid">

      <button 
        v-for="t in ['7', '8', '9', '4', '5', '6', '1', '2', '3', 'C', '0', '.']" 
        :key="t"
        :class="{ 'c-btn': t == 'C' }"
        @click="appuyer(t)"
         >
        {{ t }}

      </button>
    </div>
  </div>
</template>

<style scoped>
.card { max-width: 360px; margin: 10px auto; font-family: sans-serif; }
h1 { background: #2BB8E8; color: white; text-align: center; margin: 0; padding: 10px; font-size: 18px; }
.top { background: #2BB8E8; padding: 15px; display: flex; flex-direction: column; gap: 10px; }
.row { display: flex; justify-content: space-between; align-items: center; }
select { padding: 4px; border-radius: 4px; font-weight: bold; }
.val { font-size: 36px; border-bottom: 2px solid #000; min-width: 120px; text-align: right; }
.btn-inv { background: none; border: none; font-size: 20px; cursor: pointer; align-self: flex-start; }
.btn-conv { background: #fff; border: none; padding: 10px; font-weight: bold; border-radius: 4px; cursor: pointer; }
.err { color: red; margin: 0; font-size: 12px; text-align: center; }
.grid { display: grid; grid-template-columns: repeat(3, 1fr); padding: 10px; gap: 5px; background: #f4f4f4; }
.grid button { background: none; border: none; font-size: 22px; color: #1BA6C9; height: 40px; cursor: pointer; }
.grid button.c-btn { color: #F0727A; }
</style>