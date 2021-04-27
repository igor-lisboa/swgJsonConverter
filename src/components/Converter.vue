<template>
  <div>
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text">Put your JSON here</span>
      </div>
      <textarea class="form-control" v-model="json"></textarea>
      <div class="input-group-append">
        <button class="btn btn-warning" type="button" @click="convert">Convert</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
export default defineComponent({
  name: "Converter",
  setup: () => {
    const json = ref("{}");
    const convert = () => {
      alert(json.value);
    };
    return { json, convert };
  },
});
</script>