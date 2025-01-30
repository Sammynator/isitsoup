<script setup>
import { ref } from "vue";

const image = ref(null);
const preview = ref(null);
const result = ref(null);

const checkIfSoup = () => {
  // Only assign a result if it hasn't been set yet
  if (result.value === null) {
    result.value =
      Math.random() > 0.5 ? "Yes, this is soup! 🍜" : "No, this is NOT soup! ❌";
  }
};

const handleImageUpload = (event) => {
  const file = event.target.files[0];
  if (file) {
    preview.value = URL.createObjectURL(file);
    result.value = null; // Reset result only when a new image is uploaded
  }
};
</script>

<template>
  <div class="main">
    <div class="menu">
      <h1 class="nav">Is This Soup? 🍲</h1>

      <input
        type="file"
        @change="handleImageUpload"
        accept="image/*"
        class="dateiWahl"
      />

      <div v-if="preview" class="mb-4">
        <img
          :src="preview"
          alt="Uploaded image"
          class="w-64 h-64 object-cover rounded-lg shadow"
        />
      </div>

      <button
        @click="checkIfSoup"
        v-if="preview"
        class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-700 transition"
      >
        Check if it's soup!
      </button>

      <p v-if="result" class="mt-4 text-xl font-semibold">{{ result }}</p>
    </div>
  </div>
</template>
