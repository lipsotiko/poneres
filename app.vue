<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
<script setup lang="ts">
const url = "https://poneres.com";
const title = "Poneres.com | A Property Management Company";
const description =
  "Keeping Baltimore's rental market running smoothly. Landlords can relax knowing their investments are in qualified hands, with services covering everything from tenant placement to maintenance coordination.";

useHead({
  title,
  meta: [
    {
      property: "description",
      content: description,
    },
    {
      property: "keywords",
      content:
        "poneres, property, management, real estate, maintenance, rental, services, tenant, landlord, chicago, niles, park ridge, evanston",
    },
    {
      property: "author",
      content: "Poneres Property Management",
    },
  ],
  link: [
    {
      href: url,
      rel: "canonical",
    },
  ],
  script: [
    {
      async: true,
      src: "https://www.googletagmanager.com/gtag/js?id=G-G80494X25T"
    }, {
      src: '/js/google.js',
      type: 'text/javascript',
    }
  ]
});

useSeoMeta({
  title,
  ogUrl: url,
  ogTitle: "Poneres Property Management",
  ogDescription: description,
  ogImage: `${url}/poneres-logo.png`,
  ogImageWidth: 600,
  ogImageHeight: 600,
  ogType: "website",
});
</script>
<style lang="scss">
html {
  font-family: "RedditMono, sans-serif";
}

@font-face {
  font-family: "RedditMono";
  src: url("~/assets//RedditMono.ttf");
}
</style>
