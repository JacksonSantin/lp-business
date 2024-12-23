<template>
  <section class="container mx-auto px-4 py-16 space-y-16">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center mt-10">
      <div class="text-center md:text-left">
        <h2 class="text-2xl font-bold mb-4">TRANSPORTES</h2>
        <p class="text-lg leading-relaxed">
          Realiza transportes de máquinas e equipamentos industriais até 9
          toneladas.
        </p>
      </div>
      <div class="flex justify-center">
        <img
          src="../../assets/images/transportes/47507.jpg"
          alt="Transportes"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
definePageMeta({
  layout: 'default',
})
definePageMeta({
  middleware: ['auth'],
})
</script>
