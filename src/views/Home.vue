<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Currency Convert</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true"> 
      <div id="container">
        <Search @amount="getValue"></Search>
        <Results v-if="country" :country="country"></Results>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import Search from '@/components/Search.vue';
import Results from '@/components/Results.vue';

export default defineComponent({
 
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Search,
    Results
  },
   data(){
    return {
      country: null,
    }
  },
  methods:{
     getValue(data){
      this.country = data
    }
  },
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>