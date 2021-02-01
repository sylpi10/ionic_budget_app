<template>
   <ion-grid>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="warning">
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar color="primary">
          <ion-title size="medium">Budget App</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <div id="container">
        <ion-row class="ion-justify-content-center">
            <ion-col size-lg="6" size-sm="12">
            <ion-card>
              <!-- <div class="expense-wrapper"> -->
                <ion-card-header>
                  <ion-text clolr="warning">New Expense </ion-text>
                  </ion-card-header>
                   <ion-card-content>
                  <ion-item>
                    <ion-input type="text" placeholder="Description" clearinput="true"
                      :value="description" @ionChange="description=$event.target.value"
                     ></ion-input>
                  </ion-item>
                   </ion-card-content>
                    <ion-card-content>
                  <ion-item>
                      <ion-input class="input" type="number" placeholder="Price" 
                        :value="price" @ionChange="price=$event.target.value"></ion-input>
                  </ion-item>
                 </ion-card-content>
                  <ion-row class="ion-justify-content-end">
                   <ion-button color="danger" fill="outline" class="ion-margin-vertical"
                    @click="remove()">
                    
                  <ion-icon name="close-circle-outline"></ion-icon> Del</ion-button>
                  <ion-button expand="block" color="warning" @click.prevent="addToList()" 
                  class="ion-margin-vertical">
                    <ion-icon name="add-sharp"></ion-icon>Add an expense</ion-button>
                  </ion-row>
            </ion-card>

            <ion-card v-for="item in boughtItems" v-bind:key="item">
              <ion-card-content class="ion-text-start">
                <ion-list>
                <ion-item>
                  <ion-label>
                    {{item.description}}: {{item.price}} €
                  </ion-label>
                </ion-item>
                </ion-list>
              </ion-card-content>
            </ion-card>
            <ion-item v-if="boughtItems.length > 0">
                  <ion-label>
                    Total: {{calcTotal}} €
                  </ion-label>
            </ion-item>
            </ion-col>
        </ion-row>
      </div>
    </ion-content>
  </ion-page>
   </ion-grid>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonItem, IonList,
         IonToolbar, IonInput, IonLabel, alertController, IonText,
        IonCard, IonCardContent,  
        IonButton, IonCol, IonGrid, IonRow, IonIcon, IonCardHeader
} from '@ionic/vue';

import{addIcons}from"ionicons";
import{addSharp,closeCircleOutline}from"ionicons/icons";

addIcons({"add-sharp":addSharp,
          "close-circle-outline":closeCircleOutline 
})

import { defineComponent } from 'vue';
import { Item } from '../beans/Item';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent, IonItem, IonList, IonText,
    IonHeader, IonPage,
    IonTitle, IonToolbar,
    IonInput, IonLabel,
    IonCard, IonCardContent, IonCardHeader, 
    IonButton, IonCol, IonGrid, IonRow, IonIcon, 
    
  },
  data() {
    return {
      boughtItems: Array<Item>(),
      description: '',
      price: ""
    }
  },
  computed: {
    calcTotal(){
      if (this.boughtItems.length > 0) {
        let total = 0;
          for (const item of this.boughtItems) {
            total += parseInt(item.price);
          }
          return total;
      }
      return 0;
    },

  },
  methods: {
    async addToList(){
      if (!(typeof(this.description) === "string" && this.description.length >= 2)) {
        const alert = await alertController
        .create({
          cssClass: 'my-custom-class',
          header: 'Error',
          message: 'Description must be text and have minimum 2 chars',
          buttons: ['OK'],
        });
      return alert.present();
      }
      else if (this.price.length < 1) {
        const alert = await alertController
        .create({
          cssClass: 'my-custom-class',
          header: 'Error',
          message: 'Enter a price',
          buttons: ['OK'],
        });
         return alert.present();
      }else{
        const newItem = new Item(this.description, this.price);
        await this.boughtItems.push(newItem);
        this.description = ''; 
        this.price = ''; 
      }
    
    },
    remove(){
     this.boughtItems.splice(0, this.boughtItems.length);
    }
  }

});
</script>

<style scoped>
#container {
  text-align: center;
  width: 100%;
  margin:10px auto;
  border-radius: 8px;
  padding: 12px;
}

/* @media screen and (min-width: 640px) {
  #container{
    width: 50%;
  }
} */
ion-icon {
  --ionicon-stroke-width: 16px;
}
.expense-wrapper{
  width: 100%;
}

#container a {
  text-decoration: none;
}
.my-custom-class{
  color: red;
}
</style>