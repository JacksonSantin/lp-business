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
        class="fixed bottom-4 left-4 right-4 md:max-w-6xl md:mx-auto bg-white rounded-lg shadow-lg py-3 px-4 z-50"
      >
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
          <div class="flex items-center gap-2 flex-1">
            <h2 class="text-base font-medium text-gray-800 flex items-center gap-1">
              Sua privacidade
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="text-gray-600"
              >
                <rect width="18" height="11" x="3" y="11" rx="2" ry="2" />
                <path d="M7 11V7a5 5 0 0 1 10 0v4" />
              </svg>
            </h2>
            <p class="text-gray-600 text-sm">
              Usamos cookies para personalizar e melhorar a sua experiência. Ao
              navegar neste site, você concorda com a nossa
              <NuxtLink
                to="/politica-de-privacidade"
                class="text-red-600 underline hover:text-red-800"
              >
                Política de Privacidade
              </NuxtLink>
              .
            </p>
          </div>
          <button
            @click="handleConsent"
            class="whitespace-nowrap bg-red-700 text-white px-6 py-2 rounded-lg hover:bg-red-800 transition-colors text-sm font-medium"
          >
            Ok, entendi
          </button>
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