<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="medium">Budget App</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <div id="container">
        <div class="expense-wrapper">

            <ion-label>New Expense </ion-label>
         <ion-item>
            <ion-input type="text" placeholder="Description" v-model="item.description"></ion-input>
          </ion-item>
         <ion-item>
            <ion-input type="number" placeholder="Montant" v-model="item.price"></ion-input>
        </ion-item>
            <ion-button expand="full" color="primary" @click="addToList()">Add</ion-button>
        </div>
 
        <div class="">
            <ion-card>
              <ion-card-header>
                <ion-card-title>{{item.description}}</ion-card-title>
              </ion-card-header>
              <ion-card-content>
                Price: {{item.price}} €
              </ion-card-content>
            </ion-card>
        </div>

      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonInput, IonLabel,
        IonCard, IonCardContent, IonCardTitle, IonButton
} from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonInput,
    IonLabel,
    IonCard, IonCardContent, IonCardTitle, IonButton
  },
  data() {
    return {
     item: {
        description: "",
        price: 0,
      },
      baughtItems: []
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
  .expense-wrapper{
    width: 100%;
    margin:10px auto;
    border-radius: 8px;
    padding: 12px;
}
@media screen and (min-width: 640px) {
  .expense-wrapper{
    width: 50%;
  }
}


#container a {
  text-decoration: none;
}
</style>