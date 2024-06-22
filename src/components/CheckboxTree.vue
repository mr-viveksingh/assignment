<script setup>
import { defineProps, defineEmits } from "vue";
import CheckboxTreeItem from "./CheckboxTreeItem.vue";

defineProps({
  list: {
    type: Array,
    required: true,
  },

  value: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["updateValue"]);

const fetchCheckBoxToggle = (updateList) => {
  emit("updateValue", updateList);
};
</script>

<template>
  <ul>
    <CheckboxTreeItem
      v-for="(item, idx) in list"
      :key="idx"
      :listItem="item"
      :value="value"
      @updateValue="fetchCheckBoxToggle"
    />
  </ul>
</template>
