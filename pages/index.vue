<template>
  <div class="flex px-2 lg:p-0 flex-col items-center justify-center min-h-screen bg-cover bg-no-repeat bg-center bg-[url(@/assets/img/6708068_3399733.jpg)]">

    <!-- <div class="absolute">
      <img
       src="https://images.unsplash.com/photo-1675910568522-c187fd74d5b9?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDIyfGJvOGpRS1RhRTBZfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=60" 
       alt="bg"/>
    </div> -->

    <div class="flex flex-col items-center bg-[#ffffffdb] p-6 rounded-2xl shadow-xl w-full max-w-md relative">
      <h1 class="text-2xl font-bold text-center mb-6 text-black">Text to speech  🎤</h1>

      <!-- input-->
      <div class="relative w-full">

        <!-- <div class="absolute -bottom-[8px] -left-[8px] w-4 h-4 bg-blue-100 rotate-45 rounded-bl-[6px]"></div> -->


        <div class= "relative z-20 bg-white text-gray-800 p-4 rounded-4xl rounded-bl-none ">
          <textarea
            v-model="text"
            class="w-full bg-transparent outline-none resize-none"
            rows="3"
            placeholder="Enter ..."
          ></textarea>
        </div>

      </div>

      <!-- <div class="w-full relative z-10 -left-[12px] bg-white h-12 "></div> -->

      <!-- speed-->
      <div class="w-full flex gap-2.5 items-center justify-between mt-6 text-black text-sm">
        <label class="text-nowrap w-fit">speed 🔊 :</label>
        <input v-model="rate" type="range" min="0.5" max="2" step="0.1" class="w-full ml-3">
        <span class=" font-semibold ">{{ rate.toFixed(1) }}</span>
      </div>

      <!-- play button-->
      <button
        @click="speak"
        class="mt-8 w-full py-1.5 text-sm rounded-lg flex items-center justify-center bg-white text-black  shadow-lg transition-all duration-300 hover:bg-gray-100 cursor-pointer relative"
        :class="{ 'animate-pulse': isSpeaking }"
      >
      play
        <!-- <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-8 h-8">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-6.704-3.84A2 2 0 005 9.328v5.344a2 2 0 003.048 1.728l6.704-3.84a2 2 0 000-3.456z" />
        </svg> -->
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const text = ref<string>("");
const rate = ref<number>(1);
const isSpeaking = ref<boolean>(false);

const speak = (): void => {
  if (!text.value) {
    alert("لطفا یک متن وارد کنید!");
    return;
  }

  const speech = new SpeechSynthesisUtterance(text.value);
  speech.rate = rate.value;
  isSpeaking.value = true;

  speech.onend = () => {
    isSpeaking.value = false;
  };

  speechSynthesis.speak(speech);
};


</script>

<style scoped>
/* افکت پالس برای دکمه پخش */
@keyframes pulse {
  0% {
    transform: scale(1);
    box-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
  }
  50% {
    transform: scale(1.1);
    box-shadow: 0 0 20px rgba(59, 130, 246, 0.7);
  }
  100% {
    transform: scale(1);
    box-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
  }
}
.animate-pulse {
  animation: pulse 1.5s infinite;
}





</style>
