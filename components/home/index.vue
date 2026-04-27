<template>
  <div class="relative w-full gallery-container">
    <div
      class="flex transition-transform duration-500 ease-in-out h-full"
      :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
    >
      <div
        v-for="(image, index) in images"
        :key="index"
        class="w-full flex-shrink-0 h-full flex items-center justify-center gallery-slide"
        :style="{
          backgroundImage: `url(${image.link})`,
          backgroundPosition: 'center',
          backgroundRepeat: 'no-repeat',
        }"
      ></div>
    </div>
  </div>

  <section class="container mx-auto px-4 py-16">
    <h1 class="text-3xl font-bold text-center mb-8">A Empresa</h1>

    <div
      class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center justify-center"
    >
      <div class="flex flex-col justify-center text-justify">
        <p class="text-lg text-gray-600 mb-4">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam nisl
          mauris, tempor vel luctus ut, laoreet ut magna. Donec eget gravida
          eros. In eget laoreet enim. Morbi pellentesque a sem nec auctor.
          Nullam ac dictum tellus, sed dictum justo. Vestibulum tempor magna
          nisi, sed fermentum elit ultricies et. Sed tempus velit mi, id
          lobortis lorem tempus ac. Vestibulum gravida semper rhoncus. Fusce
          porttitor nisl arcu, in semper purus gravida quis. Nam non lorem ut
          metus rhoncus semper.
        </p>
        <p class="text-lg text-gray-600 mb-4">
          Pellentesque sit amet tristique nulla. Proin ornare ligula non nisl
          dignissim, dignissim interdum justo imperdiet. Donec accumsan dictum
          dui, id euismod nisl posuere dictum. Quisque mollis purus eget augue
          lobortis, a aliquet orci pharetra. Sed non semper libero, tincidunt
          venenatis ex. Etiam leo diam, pellentesque quis tellus ut, vestibulum
          maximus leo. Nam urna erat, sagittis imperdiet mi elementum, bibendum
          convallis libero. Fusce nulla diam, dapibus sed velit ac, hendrerit
          scelerisque sapien. Suspendisse at ultricies ex, sit amet luctus
          dolor. Ut pellentesque, neque eu feugiat lobortis, magna neque
          venenatis ipsum, in varius neque erat iaculis nisl. Ut vel imperdiet
          augue, luctus cursus purus. Orci varius natoque penatibus et magnis
          dis parturient montes, nascetur ridiculus mus. Curabitur eleifend
          augue id massa malesuada elementum.
        </p>
      </div>

      <div class="h-96 z-10 flex justify-center">
        <LMap
          ref="map"
          :zoom="zoom"
          :center="center"
          :use-global-leaflet="false"
          class="w-full h-full rounded-lg shadow-md"
        >
          <LTileLayer
            url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
            layer-type="base"
          />
          <LMarker :lat-lng="markerPosition">
            <LPopup>
              <span class="font-bold">
                LOREM IPSUM Ltda
              </span>
              <br />
              <span class="font-semibold">Endereço:</span>
              <span>
                R. Reinoldo Mate, 496 - Cidade Alta, Marau - RS, 99150-000
              </span>
            </LPopup>
          </LMarker>
        </LMap>
      </div>
    </div>
  </section>

  <section class="container mx-auto px-4 py-8">
    <h2 class="text-3xl font-bold text-center mb-6">Galeria de Imagens</h2>

    <div class="relative w-full gallery">
      <div class="overflow-hidden rounded-lg shadow-lg">
        <div
          class="flex transition-transform duration-500 ease-in-out"
          :style="{ transform: `translateX(-${currentServiceIndex * 100}%)` }"
        >
          <div
            v-for="(service, index) in imagesGallery"
            :key="index"
            class="w-full flex-shrink-0 relative"
          >
            <div
              class="w-full"
              style="height: 700px"
              :style="{
                backgroundImage: `url(${service.image})`,
                backgroundSize: 'contain',
                backgroundPosition: 'center',
                backgroundRepeat: 'no-repeat',
              }"
            ></div>
          </div>
        </div>
      </div>

      <button
        @click="prevSlide"
        class="absolute left-2 top-1/2 -translate-y-1/2 bg-red-600 hover:bg-red-600 text-white p-2 rounded-full shadow-lg transition-all"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
      </button>

      <button
        @click="nextServiceSlide"
        class="absolute right-2 top-1/2 -translate-y-1/2 bg-red-600 hover:bg-red-600 text-white p-2 rounded-full shadow-lg transition-all"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5l7 7-7 7"
          />
        </svg>
      </button>
    </div>
    <div class="hidden md:flex justify-center mt-4 gap-2">
      <button
        v-for="(_, index) in imagesGallery"
        :key="index"
        @click="goToSlide(index)"
        class="w-3 h-3 rounded-full transition-all"
        :class="currentServiceIndex === index ? 'bg-red-600' : 'bg-gray-300'"
      ></button>
    </div>
  </section>

  <section class="container mx-auto px-4 py-16">
    <div class="flex justify-center items-center">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12 w-full max-w-7xl">
        <div class="flex justify-center items-center">
          <client-only>
            <Vue3Lottie :animation-data="ContactJson" :width="450" />
          </client-only>
        </div>

        <div class="flex justify-center items-center">
          <div class="w-full max-w-md space-y-8">
            <h2 class="text-3xl font-bold text-center text-gray-900">
              Formulário de Contato
            </h2>

            <form
              ref="form"
              @submit.prevent="sendEmail"
              method="POST"
              class="space-y-6"
            >
              <div>
                <label
                  for="nome"
                  class="block text-sm font-medium text-gray-700"
                >
                  Nome
                </label>
                <input
                  id="name"
                  placeholder="Jhon Doe"
                  name="Nome"
                  type="text"
                  required
                  class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-red-500 focus:border-red-500 sm:text-sm"
                />
              </div>

              <div>
                <label
                  for="empresa"
                  class="block text-sm font-medium text-gray-700"
                >
                  Empresa
                </label>
                <input
                  id="company"
                  placeholder="LOREM IPSUM"
                  name="Empresa"
                  type="text"
                  class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-red-500 focus:border-red-500 sm:text-sm"
                />
              </div>

              <div>
                <label
                  for="telefone"
                  class="block text-sm font-medium text-gray-700"
                >
                  Telefone
                </label>
                <input
                  id="phone"
                  placeholder="(54) 9 9999-9999"
                  name="Telefone"
                  type="tel"
                  data-maska="['(##) ####-####', '(##) #####-####']"
                  v-maska
                  required
                  class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-red-500 focus:border-red-500 sm:text-sm"
                />
              </div>

              <div>
                <label
                  for="email"
                  class="block text-sm font-medium text-gray-700"
                >
                  Email
                </label>
                <input
                  id="email"
                  placeholder="[removido]"
                  name="E-mail"
                  type="email"
                  class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-red-500 focus:border-red-500 sm:text-sm"
                />
              </div>

              <div>
                <label
                  for="mensagem"
                  class="block text-sm font-medium text-gray-700"
                >
                  Mensagem
                </label>
                <textarea
                  id="message"
                  name="Mensagem"
                  placeholder="Deixe sua mensagem aqui..."
                  rows="4"
                  class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-red-500 focus:border-red-500 sm:text-sm"
                ></textarea>
              </div>

              <div>
                <button
                  type="submit"
                  class="w-full py-2 px-4 bg-red-600 text-white font-semibold rounded-md hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 sm:text-lg"
                  disabled
                >
                  Enviar
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { banner } from '~/core/const/banner'
import { gallery } from '~/core/const/gallery'
import { vMaska } from 'maska/vue'
import ContactJson from '../../assets/images/lotties/contact.json'

const zoom = ref(16)
const center = ref([-28.4458018158523, -52.20187841381167])
const markerPosition = ref([-28.4458018158523, -52.20187841381167])
const images = ref(banner)
const imagesGallery = ref(gallery)
const currentIndex = ref(0)
const currentServiceIndex = ref(0)
const totalSlides = images.value.length

function nextServiceSlide() {
  currentServiceIndex.value =
    (currentServiceIndex.value + 1) % imagesGallery.value.length
}

function prevSlide() {
  currentServiceIndex.value =
    currentServiceIndex.value === 0
      ? imagesGallery.value.length - 1
      : currentServiceIndex.value - 1
}

function goToSlide(index) {
  currentServiceIndex.value = index
}

function nextSlide() {
  currentIndex.value = (currentIndex.value + 1) % totalSlides
}

onMounted(() => {
  setInterval(() => {
    nextSlide()
  }, 5000)
})
</script>

<style scoped>
#map {
  width: 100%;
  height: 400px;
}

.h-96 {
  height: 24rem;
}

.gallery-container {
  height: 100vh;
  background-color: black;
}

.gallery {
  background-color: black;
}

.gallery-slide {
  background-size: contain;
}

@media screen and (max-width: 768px) {
  .gallery-container {
    height: 300px;
    margin-top: 5rem;
    background-color: transparent;
  }

  .gallery-slide {
    height: 100%;
    background-size: cover;
  }
}
</style>
