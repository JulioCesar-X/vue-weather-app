<template>
  <div class="relative flex items-center justify-center min-h-screen w-full overflow-hidden bg-gradient-to-r from-blue-600 to-indigo-900 dark:from-gray-900 dark:to-gray-800 transition-all animate-gradient">
    <!-- Camada escura para contraste -->
    <div class="absolute inset-0 bg-black opacity-30"></div>

    <!-- Componente de Exibição -->
    <WeatherDisplay
      :location="location"
      :weather="weather"
      :unit="unit"
      :toggleUnit="toggleUnit"
      :errorMsg="errorMsg"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import WeatherDisplay from "@/components/WeatherDisplay.vue";

const location = ref("Fetching location...");
const weather = ref({ temp: null, icon: "", description: "" });
const unit = ref("C");
const errorMsg = ref("");

const toggleUnit = () => {
  if (weather.value.temp !== null) {
    weather.value.temp = unit.value === "C"
      ? (weather.value.temp * 9/5) + 32
      : ((weather.value.temp - 32) * 5) / 9;
    unit.value = unit.value === "C" ? "F" : "C";
  }
};

const getWeather = async (lat, lon) => {
  const apiURL = `https://weather-proxy.freecodecamp.rocks/api/current?lat=${lat}&lon=${lon}`;

  try {
    const res = await fetch(apiURL);
    if (!res.ok) throw new Error("Falha ao buscar os dados.");
    const data = await res.json();

    location.value = `${data.name}, ${data.sys.country}`;
    weather.value = {
      temp: data.main.temp,
      icon: data.weather[0].icon,
      description: data.weather[0].description
    };
  } catch (error) {
    console.error("Erro ao buscar clima:", error);
    errorMsg.value = "Falha ao recuperar os dados.";
  }
};

const getLocation = () => {
  if (window.isSecureContext && navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      (pos) => getWeather(pos.coords.latitude, pos.coords.longitude),
      (err) => {
        console.error("Erro na geolocalização:", err);
        errorMsg.value = "Habilite o acesso à localização!";
      }
    );
  } else {
    errorMsg.value = "Geolocalização requer HTTPS!";
  }
};

onMounted(getLocation);
</script>

<style>
/* Gradiente animado para fundo */
@keyframes gradientAnimation {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animate-gradient {
  background-size: 200% 200%;
  animation: gradientAnimation 8s ease infinite;
}
</style>
