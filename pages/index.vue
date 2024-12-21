<template>
  <Home />
</template>

<script setup lang="ts">
const title = "DM Guinchos";
const description =
  "DM Guindastes - Marau/RS - Guindastes, Guinchos, Empilhadeiras, Transportes, Kit Remoção, Planos de Rigging - Telefone: (54)3342-5022";
const keywords =
  "guindaste,marau,guindastes,em,dmguinchos,dm guinchos, guinchos em marau,guindastes em marau,empilhadeira, guinchos,empilhadeiras,guindastes, qy70k, hyster, dmguinchos,kit remoção,remocao,dm guinchos,l9web, mauro tessaro,taura,desidério tessaro,guindaste rs,marau guindaste,marau guindastes";
const image = "/_nuxt/assets/images/logo_dm.png";

useSeoMeta(
  {
    title,
    description,
    keywords,
    ogTitle: title,
    ogDescription: description,
    ogType: "website",
    ogImage: image,
    twitterTitle: title,
    twitterDescription: description,
    twitterImage: image,
    twitterCard: "summary_large_image",
  },
  { tagPriority: 10 }
);

useHead({
  title,
  htmlAttrs: {
    lang: "pt-BR",
  },
  link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
});
</script>
