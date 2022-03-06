<template>
  <div class="container flex justify-center mx-auto">
    <ul class="flex">
      <li>
        <button
          class="h-10 px-5 text-gray-600 bg-white border border-r-0 border-gray-600 hover:bg-gray-100"
          @click="previousPage"
        >
          Prev
        </button>
      </li>
      <li>
        <button
          class="h-10 px-5 text-gray-600 bg-white border border-gray-600 hover:bg-gray-100"
          @click="nextPage"
        >
          Next
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>

const emit = defineEmits(['nextPage', "previousPage"])

const previousPage = () => {
  emit('previousPage')
}

const nextPage = () => {
  emit('nextPage')
}

</script>
