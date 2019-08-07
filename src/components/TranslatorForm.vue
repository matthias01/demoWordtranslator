<template>
  <div id="translatorForm">
    <h2>a basic form</h2> 
    
    <form @submit.prevent="formSubmit">
      <p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
  </p>
      <input type="text" v-model="text" placeholder="Enter a word">
      <select v-model="language">
        <option v-for="item in langs" :value="item.value" :key="item.value">{{ item.name }}</option>
      </select>
      <input class="btn btn-default" type="submit" value="Translate">
    </form>
  </div>
</template>

<script>
export default {
  name: 'translator',
  data(){
    return{
      errors:[],
      text:'', 
      language: 'en',
      langs:[
           {name:'English', value: 'en'},
           {name:'Russia', value: 'ru'},
           {name:'German', value: 'de'},
           {name:'Swedish', value: 'sv'},
           {name:'Japanese', value: 'ja'},
      ]
     
    }
  },
  methods:{
    formSubmit(e){
      this.errors = [];
      if(!this.text) {
        this.errors.push("sentence required.");
      }

      if(!this.errors.length) this.$emit('formSubmit', this.text, this.language);
      e.preventDefault();
    
     
    }
  },
  
}
</script>

<style>
b{
  color: red;
}
</style>
