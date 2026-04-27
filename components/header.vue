<template>
  <header :class="['fixed inset-x-0 top-0 z-50', headerClass]">
    <nav
      class="flex items-center justify-between p-6 lg:px-8"
      aria-label="Global"
    >
      <div class="flex lg:flex-1">
        <a href="/" class="-m-1.5 p-1.5">
          <span class="sr-only">LOREM IPSUM</span>
          <img
            class="h-12 w-auto"
            src="../assets/images/logo_branca.png"
            alt="Logo"
          />
        </a>
      </div>
      <div class="flex lg:hidden">
        <button
          type="button"
          class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-white"
          @click="mobileMenuOpen = true"
        >
          <span class="sr-only">Open main menu</span>
          <Bars3Icon class="size-6" aria-hidden="true" />
        </button>
      </div>
      <div class="hidden lg:flex lg:gap-x-12 lg:justify-end">
        <a
          v-for="item in navigation"
          :key="item.name"
          :href="item.href"
          class="text-sm/6 font-semibold text-white hover:text-zinc-200"
        >
          {{ item.name }}
        </a>
      </div>
    </nav>
    <Dialog
      class="lg:hidden"
      @close="mobileMenuOpen = false"
      :open="mobileMenuOpen"
    >
      <div class="fixed inset-0 z-50" />
      <DialogPanel
        class="fixed inset-y-0 right-0 z-50 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10"
      >
        <div class="flex items-center justify-between">
          <a href="/" class="-m-1.5 p-1.5">
            <span class="sr-only">LOREM IPSUM</span>
            <img
              class="h-8 w-auto"
              src="../assets/images/logo.svg"
              alt="Logo mobile"
            />
          </a>
          <button
            type="button"
            class="-m-2.5 rounded-md p-2.5 text-gray-700"
            @click="mobileMenuOpen = false"
          >
            <span class="sr-only">Close menu</span>
            <XMarkIcon class="size-6" aria-hidden="true" />
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/10">
            <div class="space-y-2 py-6">
              <a
                v-for="item in navigation"
                :key="item.name"
                :href="item.href"
                class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50"
              >
                {{ item.name }}
              </a>
            </div>
          </div>
        </div>
      </DialogPanel>
    </Dialog>
  </header>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import { Dialog, DialogPanel } from "@headlessui/vue";
import { Bars3Icon, XMarkIcon } from "@heroicons/vue/24/outline";
import { header } from "~/core/const/header";

const navigation = ref(header);
const isScrolled = ref(false);
const mobileMenuOpen = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 0;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});

const headerClass = computed(() => {
  return {
    "bg-red-600 bg-opacity-85 transform translate-y-0 opacity-100 transition-all duration-300":
      isScrolled.value,
    "bg-red-600 bg-opacity-85 transform translate-y-0 transition-all duration-300":
      !isScrolled.value,
  };
});
</script>

<style scoped>
.header {
  transition: background-color 0.3s ease, opacity 0.3s ease, transform 0.3s ease;
}

@media screen and (max-width: 768px) {
  header {
    background-color: #dc2626;
  }
}
</style>
