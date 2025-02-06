# 🌤️ Weather App - Vue + TailwindCSS

## 📌 Overview  
This is a **Weather App** built with **Vue 3** and **TailwindCSS**, featuring **real-time weather updates** based on the user's location.  
The application fetches data from a weather API and provides **temperature**, **weather conditions**, and **unit conversion (°C/°F)**.

---

## ⚙️ Features  
✅ **Live Weather Data** – Fetches real-time weather based on geolocation.  
✅ **Temperature Unit Toggle** – Easily switch between Celsius (°C) and Fahrenheit (°F).  
✅ **Modern UI with TailwindCSS** – Beautiful design with animations and a glassmorphism effect.  
✅ **Dark Mode Support** – Seamless transition between light and dark themes.  
✅ **Error Handling** – Displays alerts when location access is denied or API fails.  

---

## 🚀 Getting Started  

### 1️⃣ Install Dependencies  
Ensure you have **Node.js (v20.x.x)** installed, then install dependencies:  
```sh
npm install
```

### 2️⃣ Run the Development Server  
To start the project, use:  
```sh
npm run dev
```
Then, open `http://localhost:5173` in your browser.

```

### ✅ CSS File (`main.css`)  
Ensure TailwindCSS is imported properly:  
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### ✅ API Configuration  
The app fetches weather data from:  
```
https://weather-proxy.freecodecamp.rocks/api/current?lat={lat}&lon={lon}
```
Make sure your **browser allows geolocation** for the app to work.

---

## 📂 Project Structure  
```
src/
│── components/
│   ├── WeatherDisplay.vue  # Weather UI component
│── assets/
│   ├── main.css  # TailwindCSS styles
│── main.js  # Vue entry point
│── App.vue  # Main app component
```

---

## 📜 License  
This project is **open-source** and free to use under the MIT License.

---
