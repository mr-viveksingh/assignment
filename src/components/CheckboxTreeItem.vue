<script setup>
import { computed, defineProps, defineEmits, ref } from "vue";
const props = defineProps({
  listItem: {
    type: Object,
    required: true,
  },

  value: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["updateValue"]);

const removeList = ref([]);

const newValue = computed({
  get() {
    return props.value;
  },
  set() {
    return props.value;
  },
});

const hasChildren = computed(() => {
  return props.listItem.children && props.listItem.children.length > 0;
});

const unCheckedChildren = (list) => {
  list.forEach((item) => {
    if (item.children) {
      unCheckedChildren(item.children);
    }
    removeList.value.push(item.value);
  });
};

const toggleCheckBox = ($event) => {
  let modelValue = props.value;
  const checkedValue = $event.target.value;
  if (modelValue.includes(checkedValue)) {
    const listItem = props.listItem.children;
    if (listItem) {
      unCheckedChildren(listItem);
      modelValue = modelValue.filter((v) => !removeList.value.includes(v));
    }
    const index = modelValue.indexOf(checkedValue);
    modelValue.splice(index, 1);
  } else {
    modelValue.push(checkedValue);
  }
  onUpdateValue(modelValue);
};

const onUpdateValue = (modelValue) => {
  emit("updateValue", modelValue);
  removeList.value = [];
};

const valueOnUpdated = ($event) => {
  emit("updateValue", $event);
};
</script>

<template>
  <li>
    <div class="list-item">
      <input
        v-model="newValue"
        type="checkbox"
        :id="listItem.value"
        :name="listItem.value"
        :value="listItem.value"
        @click="toggleCheckBox($event)"
      />
      <label :for="listItem.value"> {{ listItem.label }}</label>
    </div>
    <ul v-if="hasChildren && value.includes(listItem.value)">
      <CheckboxTreeItem
        v-for="(children, idx) of listItem.children"
        :key="idx"
        :listItem="children"
        :value="value"
        @updateValue="valueOnUpdated"
      />
    </ul>
  </li>
</template>

<style>
ul {
  margin-left: 20px;
}

li {
  list-style: none;
  padding: 4px 0px;
}

.list-item {
  display: flex;
  align-items: center;
  gap: 6px;
}
</style>
