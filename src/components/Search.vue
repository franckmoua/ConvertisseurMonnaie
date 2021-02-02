<template>
  <ion-toolbar id="form">
      <ion-card>
        <ion-item position="fixed">Amount</ion-item>
        <ion-input v-model="devise.amount" type="number" modelvalue="0" @keydown.enter="getValue" placeholder="EUR"></ion-input>
      
        
        <ion-item>
        <ion-label>Convert to</ion-label>
            <ion-select v-model="devise.symbol">
                <ion-select-option v-for="(countries,name) in countries" :key="countries" :value="name">{{ countries }}</ion-select-option>
            </ion-select>
        </ion-item>
        <section>
          <ion-button expand="block" color="primary" @click.prevent="getValue">Convert</ion-button>
        </section>
      </ion-card> 
    
   </ion-toolbar>
</template>
//v-for="(countries, name) in countries"
//this shows the key of the value in the data
//ex: USD: "United States Dollar" USD is our value("name") and "United States Dollar" is our key
<script>
import { IonInput, IonButton, IonToolbar, IonLabel, IonSelect, IonSelectOption, IonItem, IonCard } from '@ionic/vue';
import axios from 'axios';
export default ({
  name: 'Search',
  data(){
    return{
      devise: {
      amount:"",
      symbol:"", 
      },
     countries:[],
    }
  },
  methods:{
    countryList(){
      //api key in .env document
      axios
      .get(
        `http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_API_KEY}`
      )
      .then((response) => {
        //fetching country names
        this.countries = response.data.symbols;
        console.log(this.countries);
      })
      .catch((error) => {
        console.log(error);
      });
    },
    getValue(){
      this.$emit('amount', this.devise);
    }
    
  },
    mounted(){
    this.countryList();

  },
  
  components: {
      IonInput,
      IonButton,
      IonToolbar,
      IonLabel,
      IonSelect,
      IonSelectOption,
      IonItem,
      IonCard
      
  }
});
</script>