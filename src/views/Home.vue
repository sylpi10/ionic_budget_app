<template>
   <ion-grid>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="primary">
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
                  <ion-label>New Expense </ion-label>
                  </ion-card-header>
                   <ion-card-content>
                  <ion-item>
                    <ion-input type="text" placeholder="Description"
                      :value="description" @ionChange="description=$event.target.value"
                     ></ion-input>
                  </ion-item>
                   </ion-card-content>
                    <ion-card-content>
                  <ion-item>
                      <ion-input class=input type="number" placeholder="Price" 
                        :value="price" @ionChange="price=$event.target.value"></ion-input>
                  </ion-item>
                 </ion-card-content>
                  <ion-row class="ion-justify-content-end">
                   <ion-button color="danger" fill="outline" class="ion-margin-vertical"
                    @click="remove()">
                    
                  <ion-icon name="close-circle-outline"></ion-icon> Del</ion-button>
                  <ion-button expand="block" color="primary" @click="addToList()" class="ion-margin-vertical">
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
           
            </ion-col>
        </ion-row>
      </div>
    </ion-content>
  </ion-page>
   </ion-grid>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonItem, IonList,
         IonToolbar, IonInput, IonLabel,
        IonCard, IonCardContent, IonCardTitle, 
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
    IonContent, IonItem, IonList,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonInput,
    IonLabel,
    IonCard, IonCardContent, IonCardHeader, IonButton, IonCol, IonGrid, IonRow, IonIcon
  },
  data() {
    return {
      boughtItems: Array<Item>(),
      description: "",
      price: ""
    }
  },
  methods: {
    async addToList(){
      const newItem = new Item(this.description, this.price);
      await this.boughtItems.push(newItem);
      this.description = "";
      this.price = "";
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
</style>