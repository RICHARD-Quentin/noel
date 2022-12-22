<template lang="pug">
  div.flex.flex-col.justify-center.items-center.h-screen.bg-slate-900.w-full.px-2
    div(v-if='scene === "Accueil"').flex.flex-col.justify-center.items-center
      p.text-6xl.text-white.font-bold.text-center.my-2(v-if="scene='Accueil'") Il semblerait que l'énigme précédente vous ai amené ici, mais pour quel raison ?
      p.text-2xl.text-white.text-center.my-2(v-if="scene='Accueil'") Peut etre que vous trouverez la reponse en entrant un code quelque part...
      button(type='button' class="w-1/3 h-12 px-4 text-2xl rounded bg-slate-800 text-white" @click="forback").mx-auto.my-2 Avancer


    div(v-if="scene === 'Code'").text-center
      h1.text-2xl.text-white.font-bold.text-center
        | Voici une enigme, entrez la reponse dans le champ ci dessous
      p.text-2xl.text-white
        | Si vous trouvez, vous pourrez decouvrir votre cadeau
      p.text-2xl.text-white
        | Si vous ne trouvez pas ou si vous vous trompez, tout le monde meurt. 
      p.text-xs.text-white
        | Nan, c'est pas vrai, on avait pas le budget..
      p.text-2xl.text-white
        | Bonne chance
      li.text-2xl.text-white
       ul 1. Je suis a la fois le père et ma mère
       ul 2. Je suis gardé par votre mère, mais a l'envers
       ul 3. La reponse se trouve peut etre dans l'adresse de ce site, voir dans le nom de l'onglet
       ul.text-slate-800(style='font-size: 0.4rem') 4. Bon.. la reponse c'est NOEL
      div.flex.flex-row.justify-center.items-center.mt-5
        input(type="text" placeholder="Code" class="w-1/2 h-12 px-4 text-2xl rounded-l-lg bg-slate-800 text-white" :value="code" @input="code = $event.target.value.toUpperCase()")
        button(type="button" class="w-1/3 h-12 px-4 text-2xl rounded-r-lg bg-slate-800 text-white" @click="checkCode")
          | Go

    div.flex.flex-col.justify-center.items-center.h-full.text-center(v-if="scene === 'Result'")
      div(v-if="isCodeValid")
        h1.text-6xl.text-white.font-bold.my-2
          | Félicitation
        p.text-2xl.text-white.my-2
          | Vous avez trouvé le bon code !
        p.text-2xl.text-white.my-2
          | Vous pouvez decouvrir votre cadeau en scannant ce QR Code !
        <div class="tenor-gif-embed" data-postid="10540459" data-share-method="host" data-aspect-ratio="1.33333" data-width="100%"><a href="https://tenor.com/view/mr-bean-wink-trust-me-%E0%A4%86%E0%A4%81%E0%A4%96-gif-10540459">Mr Bean Wink GIF</a>from <a href="https://tenor.com/search/mr+bean-gifs">Mr Bean GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>
        img(src="~/static/frame.png" alt="").mx-auto.my-2
      div(v-else)
        h1.text-6xl.text-white.font-bold.my-2
          | Dommage
        p.text-2xl.text-white.my-2
          | Ce n'est pas le bon code
        button(@click="reset()" class="w-1/2").h-12.px-4.text-2xl.rounded-lg.bg-slate-800.text-white.my-2
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
  if (code.value === 'NOEL') {
    isCodeValid.value = true
  }
}

const reset = () => {
  code.value = ''
  isCodeValid.value = false
  scene.value = 'Code'
}
</script>

