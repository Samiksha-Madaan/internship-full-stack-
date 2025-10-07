<!DOCTYPE html>
<html lang="en">
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }

    body {
      background: linear-gradient(#256c7b, #f7f7f7);
      color: #fff;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      text-align: center;
    }

    .current-weather {
      text-align: center;
      margin-bottom: 40px;
    }

    .current-weather h2 {
      font-size: 36px;
      margin-bottom: 10px;
    }

    .current-weather a img {
      width: 120px;
      height: 120px;
      transition: transform 0.3s;
    }

    .current-weather a img:hover {
      transform: scale(1.1);
    }

    .current-temp {
      font-size: 30px;
      font-weight: 600;
    }

    .weather-description {
      font-size: 26px;
      margin-top: 8px;
      text-transform: capitalize;
    }

    .details p {
      font-size: 18px;
      margin: 4px 0;
    }

    .card {
      max-width: 900px;
      background: rgba(255, 255, 255, 0.2);
      color: #fff;
      border-radius: 20px;
      padding: 30px;
      text-align: center;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    }

    .search {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 25px;
      gap: 10px;
    }

    .search input {
      border: none;
      outline: none;
      background: #ffffff;
      color: #000;
      padding: 10px 20px;
      height: 40px;
      border-radius: 8px;
      font-size: 18px;
      width: 70%;
    }

    .search button {
      border: none;
      outline: none;
      background: #fff;
      border-radius: 8px;
      width: 45px;
      height: 40px;
      cursor: pointer;
      font-size: 20px;
    }

    .forecast {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 20px;
    }

    .day {
      flex: 1;
      min-width: 120px;
      background: rgba(255, 255, 255, 0.7);
      border-radius: 12px;
      color: #000;
      padding: 10px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    }

    .day-of-week {
      font-size: 20px;
      font-weight: 500;
      margin-bottom: 5px;
    }

    .date {
      font-size: 14px;
      margin-bottom: 5px;
    }

    .day a img {
      width: 60px;
      height: 60px;
      margin: 5px 0;
      transition: transform 0.3s;
    }

    .day a img:hover {
      transform: scale(1.1);
    }

    .temp {
      font-size: 20px;
      font-weight: 600;
    }

    .error {
      display: none;
      color: red;
      font-size: 20px;
      margin-top: 10px;
    }
  </style>
</head>

<body>
  <div class="current-weather">
    <h2 class="city">Delhi</h2>
    <a href="icons/02n.png" target="_blank">
      <img src="icons/02n.png" class="weather-icon" alt="Weather icon">
    </a>
    <h1 class="current-temp">31°C</h1>
    <p class="weather-description">Rain</p>
    <div class="details">
      <p class="humidity">Humidity: 80%</p>
      <p class="wind">Wind: 15 km/h</p>
    </div>
  </div>

  <div class="card">
    <div class="search">
      <input type="text" placeholder="Search for location" spellcheck="false">
      <button id="searchBtn">&#128269;</button>
    </div>

    <div class="error">City not found</div>

    <div class="forecast">
      <div class="day">
        <p class="day-of-week">Monday</p>
        <p class="date">July 24</p>
        <a href="icons/04n.png" target="_blank">
          <img src="icons/04n.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">30°C</p>
      </div>
      <div class="day">
        <p class="day-of-week">Tuesday</p>
        <p class="date">July 25</p>
        <a href="icons/10n.png" target="_blank">
          <img src="icons/10n.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">32°C</p>
      </div>
      <div class="day">
        <p class="day-of-week">Wednesday</p>
        <p class="date">July 26</p>
        <a href="icons/50d.png" target="_blank">
          <img src="icons/50d.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">32°C</p>
      </div>
      <div class="day">
        <p class="day-of-week">Thursday</p>
        <p class="date">July 27</p>
        <a href="icons/sun.png" target="_blank">
          <img src="icons/sun.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">32°C</p>
      </div>
      <div class="day">
        <p class="day-of-week">Friday</p>
        <p class="date">July 28</p>
        <a href="icons/sun.png" target="_blank">
          <img src="icons/sun.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">32°C</p>
      </div>
      <div class="day">
        <p class="day-of-week">Saturday</p>
        <p class="date">July 29</p>
        <a href="icons/10n.png" target="_blank">
          <img src="icons/10n.png" class="weather-icon" alt="Weather Icon">
        </a>
        <p class="temp">32°C</p>
      </div>
    </div>
  </div>

  <script>
    document.addEventListener("DOMContentLoaded", () => {
      const apiKey = "YOUR_OPENWEATHERMAP_API_KEY"; 
      const apiUrl = "https://api.openweathermap.org/data/2.5/weather?&units=metric&q=";
      const forecastUrl = "https://api.openweathermap.org/data/2.5/forecast?&units=metric&q=";

      const searchBox = document.querySelector(".search input");
      const searchBtn = document.getElementById("searchBtn");

      async function getWeather(city) {
        try {
          const response = await fetch(apiUrl + city + `&appid=${apiKey}`);
          if (!response.ok) throw new Error("City not found");
          const data = await response.json();
          updateCurrentWeather(data);
        } catch (error) {
          document.querySelector(".error").style.display = "block";
        }
      }

      function updateCurrentWeather(data) {
        document.querySelector(".city").textContent = data.name;
        document.querySelector(".current-temp").textContent = Math.round(data.main.temp) + "°C";
        document.querySelector(".weather-description").textContent = data.weather[0].description;
        document.querySelector(".humidity").textContent = "Humidity: " + data.main.humidity + "%";
        document.querySelector(".wind").textContent = "Wind: " + data.wind.speed + " km/h";

        const iconCode = data.weather[0].icon;
        const iconUrl = `http://openweathermap.org/img/w/${iconCode}.png`;

        const img = document.querySelector(".current-weather img");
        const link = document.querySelector(".current-weather a");

        img.src = iconUrl;
        link.href = iconUrl;
      }

      async function getForecast(city) {
        try {
          const response = await fetch(forecastUrl + city + `&appid=${apiKey}`);
          if (!response.ok) throw new Error("Forecast not found");
          const data = await response.json();
          updateForecast(data);
        } catch (error) {
          console.error(error);
        }
      }

      function updateForecast(data) {
        const forecastList = data.list;
        const days = document.querySelectorAll(".day");

        for (let i = 0; i < days.length; i++) {
          const forecast = forecastList[i * 8];
          const iconCode = forecast.weather[0].icon;
          const iconUrl = `http://openweathermap.org/img/w/${iconCode}.png`;

          const img = days[i].querySelector("img");
          const link = days[i].querySelector("a");

          img.src = iconUrl;
          link.href = iconUrl;

          const temp = Math.round(forecast.main.temp);
          days[i].querySelector(".temp").textContent = temp + "°C";

          const date = new Date(forecast.dt * 1000);
          days[i].querySelector(".day-of-week").textContent = date.toLocaleDateString("en-US", { weekday: "long" });
          days[i].querySelector(".date").textContent = date.toLocaleDateString("en-US", { month: "short", day: "numeric" });
        }
      }

      searchBtn.addEventListener("click", () => {
        const city = searchBox.value.trim();
        if (city) {
          getWeather(city);
          getForecast(city);
        }
      });

      getWeather("Delhi");
      getForecast("Delhi");
    });
  </script>
</body>
</html>
