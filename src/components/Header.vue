<template>
  <ion-header>
    <ion-toolbar color="primary">
      <ion-img
        src="./assets/logo.png"
        slot="start"
        class="logoImg"
        alt="OnePiece Logo"
      ></ion-img>
      <ion-title style="margin: 0 auto">{{ pagename }}</ion-title>
    </ion-toolbar>
  </ion-header>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import { IonHeader, IonToolbar, IonImg, IonTitle } from "@ionic/vue";
export default defineComponent({
  name: "Header",
  props: ["pagename"],
  components: {
    IonHeader,
    IonToolbar,
    IonImg,
    IonTitle,
  },
});
</script>
<style>
.logo {
  font-size: 20px;
}

.logoImg {
  width: 100px;
}
</style>
