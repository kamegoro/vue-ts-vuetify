<template>
  <v-btn v-bind="{ ...$attrs, ...extAttrs }">
    <template v-for="(_, slotName) in $slots" #[slotName]>
      <slot :name="slotName" />
    </template>
  </v-btn>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "VwBtn",

  inheritAttrs: false,

  computed: {
    extAttrs() {
      return {};
    },
  },
});
</script>
