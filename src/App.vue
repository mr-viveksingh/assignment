<script setup>
import { ref } from "vue";
import CheckboxTree from "./components/CheckboxTree.vue";

const defaultList = [
  {
    value: "parent-1",
    label: "Parent 1",
  },
  {
    value: "parent-2",
    label: "Parent 2",
  },
  {
    value: "parent-3",
    label: "Parent 3",
  },
  {
    value: "parent-4",
    label: "Parent 4",
    children: [
      { value: "child-4-1", label: "Child 1" },
      { value: "child-4-2", label: "Child 2" },
      {
        value: "child-4-3",
        label: "Child 3",
        children: [
          { value: "sub-child-4-3-1", label: "Sub Child 1" },
          { value: "sub-child-4-3-2", label: "Sub Child 2" },
          { value: "sub-child-4-3-3", label: "Sub Child 3" },
          {
            value: "extra-child",
            label: "Extra Child",
            children: [{ value: "extra-child-1", label: "Extra Child 1" }],
          },
        ],
      },
    ],
  },
  {
    value: "parent-5",
    label: "Parent 5",
  },
  {
    value: "parent-6",
    label: "Parent 6",
    children: [{ value: "child-6-1", label: "Child 1" }],
  },
];
const selectedList = ref([]);
</script>

<template>
  <main class="main">
    <h1>Coding Task</h1>
    <CheckboxTree
      :list="defaultList"
      :value="selectedList"
      @updateValue="(value) => (selectedList = value)"
    />

    <div class="result">
      <h3>Result</h3>
      {{ selectedList }}
    </div>
  </main>

  <footer class="footer">
    <p>Developed by : <b>Vivek Singh</b></p>
  </footer>
</template>

<style>
*,
body {
  padding: 0;
  box-sizing: border-box;
  margin: 0;
}

.main {
  padding: 16px;
}

h1 {
  margin-bottom: 16px;
}

.result {
  margin: 20px;
}

h3 {
  margin: 12px 0px;
}

.footer {
  position: fixed;
  bottom: 0;
  padding: 16px;
  width: 100%;
  background: rgb(223, 221, 221);
}
</style>
