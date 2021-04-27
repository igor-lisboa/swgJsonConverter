<template>
  <div class="input-group">
    <div class="input-group-prepend">
      <span class="input-group-text">Put your JSON here</span>
    </div>
    <textarea class="form-control" v-model="json"></textarea>
    <div class="input-group-append">
      <button class="btn btn-dark" type="button" @click="beautyJson">
        Beauty
      </button>
      <button class="btn btn-warning" type="button" @click="convert">
        Convert
      </button>
    </div>
  </div>
  <template v-if="convertedSwgSchema != ''">
    <hr />
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text">Converted SWG Schema</span>
      </div>
      <textarea
        class="form-control"
        readonly
        v-model="convertedSwgSchema"
      ></textarea>
    </div>
  </template>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
export default defineComponent({
  name: "Converter",
  setup: () => {
    const json = ref("{}");
    const convertedSwgSchema = ref("");
    const beautyJson = () => {
      try {
        json.value = JSON.stringify(JSON.parse(json.value), null, 4);
      } catch (e) {
        alert(e);
      }
    };
    const buildSwgSchema = (
      obj: {
        type: string;
        property: string | undefined | null;
        example: string | number | object | undefined;
        required: boolean;
        children: any;
      },
      swgSchema: string
    ) => {
      if (swgSchema === "") {
        swgSchema +=
          '@SWG\\Schema(type="' +
          obj.type +
          '",required="' +
          obj.required +
          '", ';
      }

      if (obj.children != undefined) {
        if (obj.property != undefined) {
          swgSchema +=
            '@SWG\\Property(type="' +
            obj.type +
            '",property="' +
            obj.property +
            '",required="' +
            obj.required +
            '",';
        }
        Object.entries(obj.children).forEach((item: [string, any]) => {
          let newObj = item[1];
          newObj.property = item[0];

          swgSchema = buildSwgSchema(newObj, swgSchema);
        });
      } else {
        swgSchema +=
          '@SWG\\Property(type="' +
          obj.type +
          '",property="' +
          obj.property +
          '",example="' +
          obj.example +
          '",required="' +
          obj.required +
          '",';
      }
      swgSchema += "),";
      return swgSchema;
    };
    const convert = () => {
      let swgConverted = "";
      try {
        swgConverted = buildSwgSchema(JSON.parse(json.value), "");
      } catch (e) {
        alert(e);
      } finally {
        convertedSwgSchema.value = swgConverted;
      }
    };
    return { json, convert, convertedSwgSchema, beautyJson };
  },
});
</script>