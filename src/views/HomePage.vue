<template>
  <ion-page>
    <Header />

    <ion-content :fullscreen="true">
      <div class="carousel">
        <div
          class="slides"
          :style="{ transform: `translateX(-${state.currentSlide * 100}%)` }"
        >
          <div class="slide" v-for="slide in state.Carousel" :key="slide.id">
            <img :src="slide.image" />
          </div>
        </div>
        <button @click="nextSlide()" class="nextBtn">
          <i class="bx bx-chevron-right"></i>
        </button>
        <button @click="prevSlide()" class="prevBtn">
          <i class="bx bx-chevron-left"></i>
        </button>
      </div>
      <div class="subcategories">
        <div class="subcategory" v-for="category in state.Categories">
          <ion-card>
            <ion-card-header
              color="primary"
              style="display: flex; align-items: center; flex-direction: row"
            >
              <h2 style="font-size: 17px; text-transform: capitalize">
                {{ category.name }}
              </h2>
              <ion-img
                style="width: 50px; height: 50px"
                :src="category.image"
              ></ion-img>
            </ion-card-header>
            <ion-card-content
              style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px"
            >
              <div class="subcategorydiv">
                <ion-img style="border-radius: 5px; overflow: hidden">
                </ion-img>
              </div>
              <ion-button>View All</ion-button>
            </ion-card-content>
          </ion-card>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonPage } from "@ionic/vue";
import axios from "axios";
import { reactive } from "vue";
import Header from "../components/Header.vue";

interface Category {
  id: number;
  name: string;
  name_ar: string;
  image: string;
}

interface Slide {
  id: number;
  image: string;
  product: object;
}

const state = reactive({
  Categories: [] as Category[],
  Carousel: [] as Slide[],
  currentSlide: 0,
  slideInterval: null as NodeJS.Timeout | null,
});

async function GetData() {
  try {
    let response = await axios.get("http://localhost:5500/api/home");
    state.Carousel = response.data.Carousels;
    state.Categories = response.data.Categories;
  } catch (err) {
    console.log(err);
  }
}

function nextSlide() {
  state.currentSlide = (state.currentSlide + 1) % state.Carousel.length;

  stopSlideShow();

  startSlideShow();
}
function prevSlide() {
  state.currentSlide =
    (state.currentSlide - 1 + state.Carousel.length) % state.Carousel.length;

  stopSlideShow();

  startSlideShow();
}
function startSlideShow() {
  state.slideInterval = setInterval(nextSlide, 3000);
}
function stopSlideShow() {
  clearInterval(state.slideInterval as unknown as number);
}

GetData();
startSlideShow();
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

.homePage {
  background-color: var(--ion-color-bg);
}

.carousel {
  width: 100%;
  overflow: hidden;
  position: relative;
}

.slides {
  display: flex;
  transition: transform 0.3s ease-in-out;
  margin: 15px 0;
}

.slide {
  flex: 0 0 100%;
  text-align: center;
  height: 175px;
  overflow: hidden;
}

.slide img {
  height: 100%;
  width: 95%;
  border-radius: 10px;
}

.nextBtn {
  position: absolute;
  top: 50%;
  right: 10px;
  z-index: 99;
  font-size: 30px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  box-shadow: 0 0 2px #33333368;
  transform: translateY(-50%);
  color: var(--ion-color-primary);
  background: none;
}
.prevBtn {
  position: absolute;
  top: 50%;
  left: 10px;
  z-index: 99;
  font-size: 30px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  box-shadow: 0 0 2px #33333368;
  transform: translateY(-50%);
  color: var(--ion-color-primary);
  background: none;
}
</style>
