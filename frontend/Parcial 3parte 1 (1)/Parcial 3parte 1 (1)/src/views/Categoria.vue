<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Gestión de Elementos</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content :fullscreen="true">
        <div id="form-container">
          <ion-card>
            <ion-card-header>
              <ion-card-title>Agregar Elemento</ion-card-title>
            </ion-card-header>
            <ion-card-content>
              <ion-item>
                <ion-label position="floating">ID</ion-label>
                <ion-input v-model="newItem.id" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Nombre</ion-label>
                <ion-input v-model="newItem.nombre" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Descripción</ion-label>
                <ion-input v-model="newItem.descripcion" type="text"></ion-input>
              </ion-item>
              <ion-button expand="block" @click="addItem">Agregar Elemento</ion-button>
            </ion-card-content>
          </ion-card>
  
          <ion-card>
            <ion-card-header>
              <ion-card-title>Lista de Elementos</ion-card-title>
            </ion-card-header>
            <ion-card-content>
              <ion-list>
                <ion-item v-for="item in itemList" :key="item.id">
                  <ion-label>
                    <h2>{{ item.nombre }}</h2>
                    <p>ID: {{ item.id }}</p>
                    <p>Descripción: {{ item.descripcion }}</p>
                  </ion-label>
                </ion-item>
              </ion-list>
            </ion-card-content>
          </ion-card>
        </div>
        <ion-toast :is-open="showToast" message="Elemento añadido exitosamente" duration="3000" @ionDidDismiss="showToast = false"></ion-toast>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonItem, IonLabel, IonInput, IonButton, IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonList, IonToast } from '@ionic/vue';
  
  const newItem = ref({
    id: '',
    nombre: '',
    descripcion: ''
  });
  
  const itemList = ref([]);
  
  const showToast = ref(false);
  
  const addItem = () => {
    if (newItem.value.id && newItem.value.nombre && newItem.value.descripcion) {
      itemList.value.push({ ...newItem.value });
      newItem.value = { id: '', nombre: '', descripcion: '' };
      showToast.value = true;
    }
  };
  </script>
  
  <style scoped>
  #form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 16px;
  }
  
  ion-card {
    width: 100%;
    max-width: 500px;
  }
  
  ion-item {
    margin-bottom: 10px;
  }
  </style>
  