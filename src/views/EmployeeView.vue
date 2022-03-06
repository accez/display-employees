<template>
  <div v-if="loading === true">loading...</div>
  <div v-else>
    <CardComponent :employees="employeesData" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import CardComponent from "../components/CardComponent.vue";

let employeesData = ref([null]);
const loading = ref(true);

const fetchData = async (url) => {
  try {
    const response = await fetch(url);
    const data = await response.json();
    employeesData.value = await data.data;
    loading.value = false;
  } catch (error) {
    console.error(error);
  }
};

onMounted(() => {
  fetchData("http://dummy.restapiexample.com/api/v1/employees");
});
</script>
