<template>
  <div class="footer bg-black">
    <div class="footer-logo text-center">
      <div class="flex items-center justify-center text-center">
        <a
          class="social__item text-white"
          href="https://github.com/LariMoro20/jogo-forca"
          aria-label="GitHub"
          target="_blank"
        >
          <i class="ri-github-fill"></i>
        </a>
      </div>

      <small class="copy"
        ><a href="https://larissa-santos.vercel.app" target="_blank">
          {{ year }} &copy; by Larissa Santos</a
        ></small
      >
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";
export default defineComponent({
  setup() {
    return { year: new Date().getFullYear() };
  },
});
</script>

<style scoped>
.footer {
  padding: 10px;
}
.footer-logo-img {
  width: 120px;
}
.copy,
.copy a {
  text-decoration: none;
  color: #fff;
}
.social__item {
  text-decoration: none;
}
.social__item i {
  font-size: 30px;
}
</style>
