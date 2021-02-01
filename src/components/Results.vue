<template>
  <ion-card color="light" class="ion-padding">
    <ion-card-content>
      <ion-title>{{result}} {{country.symbol}}</ion-title>
    </ion-card-content>
  </ion-card>
</template>

<script>
import {  IonCard, IonCardContent, IonTitle } from '@ionic/vue';
import axios from 'axios';
export default({
  name: 'Results',
  props: ['country'],
  data(){
    return{
      result:"",
    }
  },
  components: {
    IonCard,
    IonCardContent,
    IonTitle
  },

  methods: {
    //fetching API from fixer
    convertValue(){
      axios
      .get(
        `http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_API_KEY}&symbols=${this.country.symbol}`
      )
      .then((response) => {
        //this.rate is the currency and symbol of the country selected
        //this.result calculates the selected country rate with the amount we wish to convert
        this.rate = response.data.rates[this.country.symbol]
        this.result = Math.round((this.rate * this.country.amount) * 100) / 100
        //console.log(rate)
        //console.log(this.result)
      })
      .catch((error) => {
        console.log(error);
      });
    },
  },
  mounted(){
    this.convertValue();
  },
  //Change amounts without refreshing the page
  watch: {
    country: {
      deep: true,
      handler(){
        this.convertValue();
      }
    }
  },

  });
</script>