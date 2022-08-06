<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <router-view />
      <Footer />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import Footer from "components/Parts/Footer.vue";
export default defineComponent({
  name: "MainLayout",
  components: { Footer },
  setup() {},
});
</script>
