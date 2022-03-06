<template>
  <div class="grid grid-cols-3 md:grid-cols-3 gap-3">
    <div
      v-for="employee in updateVisibleEmployees()"
      :key="employee.id"
      class="py-6 flex flex-col sm:py-12"
    >
      <div class="flex space-x-4 px-4 justify-around">
        <!-- CARD -->
        <div
          class="bg-gradient-to-b from-orange-500 to-yellow-300 h-72 w-28 md:w-96 md:rounded-3xl rounded-full shadow-md relative flex flex-col items-center justify-between md:items-start py-5 md:p-5 transition-all duration-150"
        >
          <!-- IMG PROFILE -->
          <img
            class="rounded-full w-16 h-16 absolute -top-8 transform md:scale-110 duration-700"
            :src="getAvatar(employee.employee_name)"
            :alt="employee.employee_name"
          />
          <!-- TEXTS -->
          <div
            class="transform -rotate-90 md:rotate-0 align-middle text-2xl font-semibold text-white text-center m-auto md:m-0 md:mt-8"
          >
            {{ employee.employee_name }}
          </div>
          <ul class="text-lg text-white font-light hidden md:block">
            <li>Salary: {{ employee.employee_salary }} 💸</li>
            <li>Age: {{ employee.employee_age }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
      <Paginator @nextPage="nextPage" @previousPage="previousPage" />

</template>

<script setup>
import { ref } from "vue";
import Paginator from "./PaginatorComponent.vue";

const props = defineProps({
  employees: {
    type: Array,
    required: true,
  },
});

const itemsPerPage = ref(6);
const currentPage = ref(0);
const totalPages = props.employees.length / itemsPerPage.value

const nextPage = () => {
  if (currentPage.value < totalPages - 1) {
    console.log(currentPage.value)
     currentPage.value++
  }
}

const previousPage = () => {
  if(currentPage.value === 0){return}
  currentPage.value--
}

const updateVisibleEmployees = () => {
  return props.employees.slice(
    (currentPage.value * itemsPerPage.value),
    (currentPage.value * itemsPerPage.value) + itemsPerPage.value
  );
};

const getAvatar = (employees) => {
  let splitName = employees.split(" ");
  let url = `https://avatars.dicebear.com/api/initials/${splitName[0]}%20${splitName[1]}.svg?background=orange`;
  return url;
};
</script>
