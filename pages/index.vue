<template lang="pug">
  div.flex.flex-col.justify-center.items-center.h-screen.bg-slate-900.w-full.px-2
    div(v-if='scene === "Accueil"').flex.flex-col.justify-center.items-center
      p.text-6xl.text-white.font-bold.text-center.my-2(v-if="scene='Accueil'") Il semblerait que le medaillon vous ai amené ici, mais pour quel raison ?
      p.text-2xl.text-white.text-center.my-2(v-if="scene='Accueil'") Peut etre que vous trouverez la reponse en entrant un code quelque part...
      button(type='button' class="w-1/3 h-12 px-4 text-2xl rounded bg-slate-800 text-white" @click="forback").mx-auto.my-2 Avancer


    div(v-if="scene === 'Code'").text-center
      h1.text-6xl.text-white.font-bold.text-center
        | Entrez votre code
      p.text-2xl.text-white
        | Et découvrez votre cadeau.. peut etre ?
      div.flex.flex-row.justify-center.items-center.mt-5
        input(type="text" placeholder="Code" class="w-1/2 h-12 px-4 text-2xl rounded-l-lg bg-slate-800 text-white" v-model="code")
        button(type="button" class="w-1/3 h-12 px-4 text-2xl rounded-r-lg bg-slate-800 text-white" @click="checkCode")
          | Go

    div.flex.flex-col.justify-center.items-center.h-full.text-center(v-if="scene === 'Result'")
      div(v-if="isCodeValid")
        h1.text-6xl.text-white.font-bold
          | Félicitation
        p.text-2xl.text-white
          | Vous avez trouvé le cadeau de Noel
        p.text-2xl.text-white
          | Vous pouvez le récupérer en magasin
        p.text-2xl.text-white
          | A bientot
        img(src="~/static/frame.png" alt="").mx-auto
      div(v-else)
        h1.text-6xl.text-white.font-bold
          | Dommage
        p.text-2xl.text-white
          | Ce n'est pas le bon code
        button(@click="reset()" class="w-1/2").h-12.px-4.text-2xl.rounded-lg.bg-slate-800.text-white
          | Réessayer
      
        
</template>

<script setup lang="ts">
import { ref } from 'vue'

const code = ref('')
const isCodeValid = ref(false)
const scene = ref('Accueil')

const forback = () => {
  console.log('forback')
  scene.value = 'Code'
}

const checkCode = () => {
  scene.value = 'Result'
  if (code.value === '1234') {
    isCodeValid.value = true
  }
}

const reset = () => {
  code.value = ''
  isCodeValid.value = false
  scene.value = 'Code'
}
</script>

