<template>
  <footer class="w-full">
    <div class="mx-auto max-w-7xl w-full px-4 py-8 sm:px-6 lg:px-8">
      <div
        class="grid grid-cols-1 gap-12 sm:grid-cols-2 lg:grid-cols-4 justify-items-center"
      >
        <div class="flex flex-col space-y-4 w-full max-w-xs">
          <div class="flex items-center">
            <img
              src="../assets/images/logo_dm.png"
              alt="Logo"
              class="h-8 w-auto"
            />
          </div>
          <p class="text-justify text-gray-600">
            A <b>DM GUINCHOS</b> atua no mercado prestando serviços de qualidade
            com a mais alta segurança.
          </p>
        </div>

        <div class="flex flex-col space-y-4 w-full max-w-xs">
          <h3 class="text-lg font-semibold text-gray-900">Endereço</h3>
          <address class="flex flex-col space-y-2 not-italic">
            <p class="text-sm text-gray-600">Rua Reinoldo Matte, nº 496</p>
            <p class="text-sm text-gray-600">Cidade Alta</p>
            <p class="text-sm text-gray-600">Marau - RS</p>
            <p class="text-sm text-gray-600">CEP: 99150-000</p>
          </address>
          <div class="flex items-center justify-start gap-x-6">
            <a 
              href="https://www.google.com/maps/dir/?api=1&destination=-28.4458018158523,-52.20187841381167" 
              target="_blank"
              rel="noopener noreferrer"
              aria-label="Como chegar"
              class="rounded-md bg-red-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-red-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-red-600"
            >
              COMO CHEGAR
            </a>
          </div>
        </div>

        <div class="flex flex-col space-y-4 w-full max-w-xs">
          <h3 class="text-lg font-semibold text-gray-900">Contato</h3>
          <div class="flex flex-col space-y-2">
            <p class="text-sm text-gray-600">
              <span class="font-medium">WhatsApp:</span> (54) 9 9627-1996
            </p>
            <p class="text-sm text-gray-600">
              <span class="font-medium">Mauro:</span> (54) 9 9998-0883
            </p>
            <p class="text-sm text-gray-600">
              <span class="font-medium">Desiderio:</span> (54) 9 9981-8965
            </p>
            <div class="flex flex-col space-y-1">
              <span class="font-medium">Emails: </span>
              <p class="text-sm text-gray-600">
                <a href="mailto:dmguinchos@dmguinchos.com.br"
                  >dmguinchos@dmguinchos.com.br</a
                >
              </p>
              <p class="text-sm text-gray-600">
                <a href="mailto:mauro@dmguinchos.com.br"
                  >mauro@dmguinchos.com.br</a
                >
              </p>
            </div>
          </div>
        </div>

        <div class="flex flex-col space-y-4 w-full max-w-xs">
          <h3 class="text-lg font-semibold text-gray-900">Redes Sociais</h3>
          <div class="flex space-x-6">
            <a
              href="https://wa.me/5554996271996"
              target="_blank"
              class="text-gray-500 hover:text-gray-800"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-6 h-6"
                viewBox="0 0 24 24"
                fill="currentColor"
              >
                <path :d="mdiWhatsapp" />
              </svg>
            </a>
            <a
              href="https://www.instagram.com/dmguinchos"
              target="_blank"
              class="text-gray-500 hover:text-gray-800"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-6 h-6"
                viewBox="0 0 24 24"
                fill="currentColor"
              >
                <path :d="mdiInstagram" />
              </svg>
            </a>
            <a
              href="https://www.facebook.com/p/DM-Guinchos-100068169376941"
              target="_blank"
              class="text-gray-500 hover:text-gray-800"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-6 h-6"
                viewBox="0 0 24 24"
                fill="currentColor"
              >
                <path :d="mdiFacebook" />
              </svg>
            </a>
            <a
              href="https://www.linkedin.com/in/mauro-guinchos-tessaro-938a4669"
              target="_blank"
              class="text-gray-500 hover:text-gray-800"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="w-6 h-6"
                viewBox="0 0 24 24"
                fill="currentColor"
              >
                <path :d="mdiLinkedin" />
              </svg>
            </a>
          </div>
        </div>
      </div>

      <div class="mt-12 border-t border-gray-200 pt-8">
        <p class="text-center text-sm text-gray-600">
          &copy; {{ currentYear }} DM Guinchos. Todos os direitos reservados.
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { mdiWhatsapp, mdiInstagram, mdiFacebook, mdiLinkedin } from "@mdi/js";
import dayjs from "dayjs";

const currentYear = dayjs().year();
</script>
