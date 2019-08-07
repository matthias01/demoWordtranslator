<template>
  <div id="app">
    <div class="container">
       <h2>Translator</h2>
    <h5>Lets get started</h5>
    <TranslatorForm v-on:formSubmit="TranslateText"></TranslatorForm>
    <TranslatorDisplay v-text="translation"></TranslatorDisplay>
    </div>
   
   
  </div>
</template>

<script>
import TranslatorForm from './components/TranslatorForm.vue';
import TranslatorDisplay from './components/TranslatorDisplay.vue';
import axios from 'axios';


export default {
  name: 'app',
  components: {
   TranslatorForm, TranslatorDisplay,
  },
  data(){
    return {
       appkey : 'trnsl.1.1.20190807T075839Z.4ee9b2925601a268.855d56ee79afbcd3dab7e235b7c2e1c0c19c1134',
       translation : '',
    }
  },
  methods:{
    TranslateText(text, language){
       
     // console.log(language);
     axios.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key='+this.appkey+'&lang='+language+'&text='+text)
     .then( (response) => {
        this.translation = response.data.text[0]
     })
     .catch((err) => {
       console.log(err)
     });
    }
  }
}
</script>

<style>
#app {
 
}
</style>
