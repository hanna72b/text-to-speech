<script setup lang="ts">
import { ref } from "vue";

const text = ref<string>("");
const rate = ref<number>(1);

const speak = (): void => {
  if (!text.value) {
    alert("لطفا یک متن وارد کنید!");
    return;
  }

  const speech = new SpeechSynthesisUtterance(text.value);
  speech.rate = rate.value;
  speechSynthesis.speak(speech);
};
</script>


<template>
    <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-6">
      <div class="bg-white p-6 rounded-2xl shadow-xl w-full max-w-lg">
        <h1 class="text-2xl font-bold text-center mb-4">🎤 تبدیل متن به گفتار</h1>
        <textarea
          v-model="text"
          class="w-full p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
          rows="4"
          placeholder="متن خود را وارد کنید..."
        ></textarea>
  
        <div class="mt-4 flex items-center space-x-2">
          <label> 🔊 سرعت: </label>
          <input v-model="rate" type="range" min="0.5" max="2" step="0.1" class="w-full">
          <span>{{ rate }}</span>
        </div>
  
        <button
          @click="speak"
          class="mt-4 w-full bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600 transition"
        >
          پخش صدا
        </button>
      </div>
    </div>
  </template>
  
 