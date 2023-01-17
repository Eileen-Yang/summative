<script setup>
import { useRouter } from "vue-router";
import Siteheader from '../components/SiteHeader.vue'
import Sitehero from '../components/SiteHero.vue'
import Sitefooter from '../components/SiteFooter.vue'

const router = useRouter();
</script>

<template>
  <div class="home-container">
    <Suspense>
      <Siteheader />
    </Suspense>
    <Suspense>
      <Sitehero />
    </Suspense>
    <Suspense>
      <Sitefooter />
    </Suspense>
  </div>
</template>

<style scoped>
</style>