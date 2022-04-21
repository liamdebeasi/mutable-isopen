<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
    
      isOpen ref state: {{ isOpenRef }}<br />
      isOpen Web Component property: {{ isOpenProp }}<br />
      <ion-button @click="openModal">Open Modal</ion-button>
      
      <ion-modal
        ref="modalRef"
        :is-open="isOpenRef"
        @didPresent="updateState"
        @didDismiss="updateState"
      >
        <ion-content>Modal Content</ion-content>
      </ion-modal>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonModal, IonButton, IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'HomePage',
  components: {
    IonModal,
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton
  },
  setup() {
    const isOpenRef = ref(false);
    const isOpenProp = ref(false);
    const modalRef = ref();
    
    const updateState = () => {
      requestAnimationFrame(() => {
        isOpenProp.value = modalRef.value.$el.isOpen;
      });
    }
    
    const openModal = () => {
      isOpenRef.value = true;
    }
    
    return { isOpenRef, openModal, updateState, modalRef, isOpenProp }
  }
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
