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
          Fundada em janeiro de 2001, pelos irmãos e sócios
          <b>Desidério e Mauro Tessaro</b>, a empresa
          <b>DM Guinchos e Equipamentos Industriais Ltda</b>, atua na locação e
          prestação de serviços de guincho, empilhadeira e guindaste para
          montagens de obras e transporte especial de peças.
        </p>
        <p class="text-lg text-gray-600 mb-4">
          Atualmente, conta com 06 caminhões munck de diversas capacidades, 03
          guindastes com capacidades de 25, 30 e 90 toneladas, além de
          empilhadeiras, paleteiras, kit remoção de 20 e 40 e containers.
        </p>
        <p class="text-lg text-gray-600 mb-4">
          Para melhor atender as necessidades do contratante, contamos com os
          equipamentos mais modernos e tecnológicos do mercado.
        </p>
        <p class="text-lg text-gray-600 mb-4">
          Os serviços prestados atendem os mais altos padrões de qualidade e
          segurança.
        </p>
        <p class="text-lg text-gray-600">
          Na <b>DM Guinchos</b>, prezamos pela excelência em tudo o que fazemos,
          oferecendo serviços com <b>qualidade</b>, <b>onfiança</b> e
          <b>segurança</b>, sempre comprometidos com as necessidades e a
          satisfação dos nossos clientes.
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
                DM Guinchos e Equipamentos Industriais Ltda
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

  <section class="container mx-auto px-4 py-16">
    <h2 class="text-3xl font-bold text-center mb-8">Galeria de Imagens</h2>
    
    <div class="relative w-full">
      <div class="overflow-hidden rounded-lg shadow-lg">
        <div
          class="flex transition-transform duration-500 ease-in-out"
          :style="{ transform: `translateX(-${currentServiceIndex * 100}%)` }"
        >
          <div
            v-for="(service, index) in services"
            :key="index"
            class="w-full flex-shrink-0 relative"
          >
            <div
              class="aspect-video w-full"
              :style="{
                backgroundImage: `url(${service.image})`,
                backgroundSize: 'cover',
                backgroundPosition: 'center',
              }"
            >
            </div>
          </div>
        </div>
      </div>

      <button 
        @click="prevSlide"
        class="absolute left-2 top-1/2 -translate-y-1/2 bg-white/80 hover:bg-white text-gray-800 p-2 rounded-full shadow-lg transition-all"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
      </button>

      <button 
        @click="nextServiceSlide"
        class="absolute right-2 top-1/2 -translate-y-1/2 bg-white/80 hover:bg-white text-gray-800 p-2 rounded-full shadow-lg transition-all"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>

      <div class="flex justify-center mt-4 gap-2">
        <button
          v-for="(_, index) in services"
          :key="index"
          @click="goToSlide(index)"
          class="w-3 h-3 rounded-full transition-all"
          :class="currentServiceIndex === index ? 'bg-red-600' : 'bg-gray-300'"
        ></button>
      </div>
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

            <form ref="form" @submit.prevent="sendEmail" method="POST" class="space-y-6">
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
                  placeholder="DM Guinchos"
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
                  placeholder="jhondoe@exemplo.com.br"
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
import { ref, onMounted } from "vue";
import { banner } from "~/core/const/banner";
import { images } from "~/core/const/images";
import { vMaska } from "maska/vue";
import Swal from "sweetalert2";
import ContactJson from "../../assets/images/lotties/contact.json";

const zoom = ref(16);
const center = ref([-28.4458018158523, -52.20187841381167]);
const markerPosition = ref([-28.4458018158523, -52.20187841381167]);
const images = ref(banner);
const gallery = ref(images);
const gallery = ref()
const currentIndex = ref(0);
const currentServiceIndex = ref(0);
const totalSlides = images.value.length;

function nextServiceSlide() {
  currentServiceIndex.value = (currentServiceIndex.value + 1) % services.value.length;
}

function prevSlide() {
  currentServiceIndex.value = currentServiceIndex.value === 0 
    ? services.value.length - 1 
    : currentServiceIndex.value - 1;
}

function goToSlide(index) {
  currentServiceIndex.value = index;
}

function nextSlide() {
  currentIndex.value = (currentIndex.value + 1) % totalSlides;
}

onMounted(() => {
  setInterval(() => {
    nextSlide();
  }, 5000);
});
</script>

<script>
import emailjs from "@emailjs/browser";

export default {
  methods: {
    sendEmail() {
      const formElement = this.$refs.form;
      emailjs
        .sendForm(
          "gmailMessage",
          "template_rdu5oja",
          formElement,
          "user_0VFYQ4JjMn4RkCcdx9GRB"
        )
        .then(
          async () => {
            await Swal.fire({
              title: "Obrigado :)",
              text: "Mensagem enviada com sucesso!",
              icon: "success",
            });
            window.location.reload();
          },
          () => {
            Swal.fire({
              title: "Oops :(",
              text: "Mensagem não enviada, tente novamente!",
              icon: "error",
            });
          }
        );
    },
  },
};
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
