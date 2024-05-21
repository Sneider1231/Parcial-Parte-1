<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Gestión de Carros</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content :fullscreen="true">
        <div id="form-container">
          <ion-card>
            <ion-card-header>
              <ion-card-title>Agregar Carro</ion-card-title>
            </ion-card-header>
            <ion-card-content>
              <ion-item>
                <ion-label position="floating">ID</ion-label>
                <ion-input v-model="newCar.id" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Marca</ion-label>
                <ion-input v-model="newCar.marca" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Modelo</ion-label>
                <ion-input v-model="newCar.modelo" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Placa</ion-label>
                <ion-input v-model="newCar.placa" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Color</ion-label>
                <ion-input v-model="newCar.color" type="text"></ion-input>
              </ion-item>
              <ion-item>
                <ion-label position="floating">Categoría ID</ion-label>
                <ion-input v-model="newCar.categoriaId" type="text"></ion-input>
              </ion-item>
              <ion-button expand="block" @click="addCar">Agregar Carro</ion-button>
            </ion-card-content>
          </ion-card>
  
          <ion-card>
            <ion-card-header>
              <ion-card-title>Lista de Carros</ion-card-title>
            </ion-card-header>
            <ion-card-content>
              <ion-list>
                <ion-item v-for="car in carList" :key="car.id">
                  <ion-label>
                    <h2>{{ car.marca }} - {{ car.modelo }}</h2>
                    <p>ID: {{ car.id }}</p>
                    <p>Placa: {{ car.placa }}</p>
                    <p>Color: {{ car.color }}</p>
                    <p>Categoría ID: {{ car.categoriaId }}</p>
                  </ion-label>
                </ion-item>
              </ion-list>
            </ion-card-content>
          </ion-card>
        </div>
        <ion-toast :is-open="showToast" message="Carro añadido exitosamente" duration="3000" @ionDidDismiss="showToast = false"></ion-toast>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonItem, IonLabel, IonInput, IonButton, IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonList, IonToast } from '@ionic/vue';
  
  const newCar = ref({
    id: '',
    marca: '',
    modelo: '',
    placa: '',
    color: '',
    categoriaId: ''
  });
  
  const carList = ref([]);
  
  const showToast = ref(false);
  
  const addCar = () => {
    if (newCar.value.id && newCar.value.marca && newCar.value.modelo && newCar.value.placa && newCar.value.color && newCar.value.categoriaId) {
      carList.value.push({ ...newCar.value });
      newCar.value = { id: '', marca: '', modelo: '', placa: '', color: '', categoriaId: '' };
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
  
  
  