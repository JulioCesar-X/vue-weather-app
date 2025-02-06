<template>
  <div class="relative z-10 w-full max-w-2xl p-10 bg-white/10 dark:bg-gray-900/70 backdrop-blur-md shadow-2xl rounded-2xl text-center border border-gray-200/30 transition-all">

    <!-- Título -->
    <h1 class="text-4xl font-extrabold text-white tracking-wide animate-fadeIn">
      🌤️ Weather App
    </h1>

    <!-- Localização -->
    <p class="mt-4 text-lg text-gray-100 font-medium" v-if="location">
      📍 {{ location }}
    </p>

    <!-- Ícone do Clima -->
    <div v-if="weather.icon" class="mt-6 flex justify-center">
      <img :src="weather.icon" class="w-32 h-32 drop-shadow-lg transition-all duration-300 animate-fadeIn">
    </div>

    <!-- Temperatura -->
    <p class="text-6xl font-bold mt-6 text-white transition-all animate-fadeIn" v-if="weather.temp">
      {{ Math.round(weather.temp) }}°{{ unit }}
    </p>

    <!-- Botão para Trocar Unidade -->
    <button @click="toggleUnit"
      class="mt-6 px-6 py-3 bg-blue-500 hover:bg-blue-400 text-white font-semibold rounded-full shadow-lg transform hover:scale-105 transition-all duration-300">
      🔄 Switch to {{ unit === 'C' ? '°F' : '°C' }}
    </button>

    <!-- Descrição do Clima -->
    <p v-if="weather.description" class="mt-6 text-lg text-gray-300 font-light italic">
      {{ weather.description }}
    </p>

    <!-- Mensagem de Erro -->
    <p v-if="errorMsg" class="mt-6 text-lg text-red-400 font-semibold">
      ⚠️ {{ errorMsg }}
    </p>
  </div>
</template>

<script setup>
defineProps(["location", "weather", "unit", "toggleUnit", "errorMsg"]);
</script>

<style>
/* Animação de Fade-In */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fadeIn {
  animation: fadeIn 1s ease-in-out;
}
</style>
