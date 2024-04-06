<template>
  <ion-header>
    <ion-toolbar color="primary">
      <ion-img
        src="./assets/logo.png"
        slot="start"
        class="logoImg"
        alt="OnePiece Logo"
      ></ion-img>
    </ion-toolbar>
  </ion-header>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import { IonHeader, IonToolbar, IonImg } from "@ionic/vue";
export default defineComponent({
  name: "Header",
  components: {
    IonHeader,
    IonToolbar,
    IonImg,
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
