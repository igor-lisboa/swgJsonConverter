<template>
  <div class="d-flex h-100 text-center text-white bg-dark">
    <div class="cover-container d-flex w-100 h-100 p-3 mx-auto flex-column">
      <header class="mb-auto row">
        <h3 class="float-md-start mb-0 mx-2 text-white">SWG JSON CONVERTER</h3>
      </header>

      <main class="px-3">
        <converter />
      </main>

      <footer class="mt-auto text-white-50">
        <p>
          Developed by
          <a
            href="https://github.com/igor-lisboa"
            target="_blank"
            class="text-white"
            >LISBÔA, Igor</a
          >.
        </p>
      </footer>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import Converter from "./components/Converter.vue";
export default defineComponent({
  components: { Converter },
  name: "App",
});
</script>
<style>
html,
body,
#app {
  height: 100%;
  width: 100%;
  margin: 0px;
  padding: 0px;
}
#app {
  display: grid;
}
</style>