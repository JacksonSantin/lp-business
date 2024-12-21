<!-- components/CookieConsent.vue -->
<template>
  <ClientOnly>
    <Transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="transform translate-y-full opacity-0"
      enter-to-class="transform translate-y-0 opacity-100"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="transform translate-y-0 opacity-100"
      leave-to-class="transform translate-y-full opacity-0"
    >
      <div
        v-if="isVisible"
        class="fixed bottom-4 left-4 right-4 md:max-w-2xl md:mx-auto bg-white rounded-lg shadow-lg p-6 m-4 z-50 border border-gray-200"
      >
        <div class="flex items-start gap-3">
          <div class="w-5 h-5 text-gray-600 mt-1 flex-shrink-0">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <rect width="18" height="11" x="3" y="11" rx="2" ry="2" />
              <path d="M7 11V7a5 5 0 0 1 10 0v4" />
            </svg>
          </div>
          <div class="flex-1">
            <h2 class="text-lg font-semibold text-gray-800 mb-2">
              Sua privacidade
            </h2>
            <p class="text-gray-600 mb-4">
              Usamos cookies para personalizar e melhorar a sua experiência. Ao
              navegar neste site, você concorda com a nossa
              <NuxtLink
                to="/politica-de-privacidade"
                class="text-red-600 hover:text-red-700 underline"
              >
                Política de Privacidade
              </NuxtLink>
              .
            </p>
            <button
              @click="handleConsent"
              class="bg-red-600 text-white px-6 py-2 rounded-md hover:bg-red-700 transition-colors"
            >
              Ok, entendi
            </button>
          </div>
        </div>
      </div>
    </Transition>
  </ClientOnly>
</template>

<script setup>
const isVisible = ref(true);

onMounted(() => {
  const hasConsented = localStorage.getItem('cookieConsent');
  if (hasConsented) {
    isVisible.value = false;
  }
});

const handleConsent = () => {
  localStorage.setItem('cookieConsent', 'true');
  isVisible.value = false;
};
</script>