<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="1">
        <div class="weatherWidget">
          <v-img
            :src="formattedWeather.weather.image"
            height="80px"
            width="80px"
          ></v-img>
          {{ formattedWeather.temperature }}
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "weatherWidget",
  data() {
    return {
      weatherCodes: [
        {
          0: {
            day: {
              description: "Sunny",
              image: "http://openweathermap.org/img/wn/01d@2x.png",
            },
            night: {
              description: "Clear",
              image: "http://openweathermap.org/img/wn/01n@2x.png",
            },
          },
          1: {
            day: {
              description: "Mainly Sunny",
              image: "http://openweathermap.org/img/wn/01d@2x.png",
            },
            night: {
              description: "Mainly Clear",
              image: "http://openweathermap.org/img/wn/01n@2x.png",
            },
          },
          2: {
            day: {
              description: "Partly Cloudy",
              image: "http://openweathermap.org/img/wn/02d@2x.png",
            },
            night: {
              description: "Partly Cloudy",
              image: "http://openweathermap.org/img/wn/02n@2x.png",
            },
          },
          3: {
            day: {
              description: "Cloudy",
              image: "http://openweathermap.org/img/wn/03d@2x.png",
            },
            night: {
              description: "Cloudy",
              image: "http://openweathermap.org/img/wn/03n@2x.png",
            },
          },
          45: {
            day: {
              description: "Foggy",
              image: "http://openweathermap.org/img/wn/50d@2x.png",
            },
            night: {
              description: "Foggy",
              image: "http://openweathermap.org/img/wn/50n@2x.png",
            },
          },
          48: {
            day: {
              description: "Rime Fog",
              image: "http://openweathermap.org/img/wn/50d@2x.png",
            },
            night: {
              description: "Rime Fog",
              image: "http://openweathermap.org/img/wn/50n@2x.png",
            },
          },
          51: {
            day: {
              description: "Light Drizzle",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Light Drizzle",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          53: {
            day: {
              description: "Drizzle",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Drizzle",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          55: {
            day: {
              description: "Heavy Drizzle",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Heavy Drizzle",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          56: {
            day: {
              description: "Light Freezing Drizzle",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Light Freezing Drizzle",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          57: {
            day: {
              description: "Freezing Drizzle",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Freezing Drizzle",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          61: {
            day: {
              description: "Light Rain",
              image: "http://openweathermap.org/img/wn/10d@2x.png",
            },
            night: {
              description: "Light Rain",
              image: "http://openweathermap.org/img/wn/10n@2x.png",
            },
          },
          63: {
            day: {
              description: "Rain",
              image: "http://openweathermap.org/img/wn/10d@2x.png",
            },
            night: {
              description: "Rain",
              image: "http://openweathermap.org/img/wn/10n@2x.png",
            },
          },
          65: {
            day: {
              description: "Heavy Rain",
              image: "http://openweathermap.org/img/wn/10d@2x.png",
            },
            night: {
              description: "Heavy Rain",
              image: "http://openweathermap.org/img/wn/10n@2x.png",
            },
          },
          66: {
            day: {
              description: "Freezing Rain",
              image: "http://openweathermap.org/img/wn/10d@2x.png",
            },
            night: {
              description: "Freezing Rain",
              image: "http://openweathermap.org/img/wn/10n@2x.png",
            },
          },
          67: {
            day: {
              description: "Freezing Rain",
              image: "http://openweathermap.org/img/wn/10d@2x.png",
            },
            night: {
              description: "Freezing Rain",
              image: "http://openweathermap.org/img/wn/10n@2x.png",
            },
          },
          71: {
            day: {
              description: "Light Snow",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Light Snow",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          73: {
            day: {
              description: "Snow",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Snow",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          75: {
            day: {
              description: "Heavy Snow",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Heavy Snow",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          77: {
            day: {
              description: "Snow Grains",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Snow Grains",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          80: {
            day: {
              description: "Light Showers",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Light Showers",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          81: {
            day: {
              description: "Showers",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Showers",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          82: {
            day: {
              description: "Heavy Showers",
              image: "http://openweathermap.org/img/wn/09d@2x.png",
            },
            night: {
              description: "Heavy Showers",
              image: "http://openweathermap.org/img/wn/09n@2x.png",
            },
          },
          85: {
            day: {
              description: "Snow Showers",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Snow Showers",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          86: {
            day: {
              description: "Snow Showers",
              image: "http://openweathermap.org/img/wn/13d@2x.png",
            },
            night: {
              description: "Snow Showers",
              image: "http://openweathermap.org/img/wn/13n@2x.png",
            },
          },
          95: {
            day: {
              description: "Thunderstorm",
              image: "http://openweathermap.org/img/wn/11d@2x.png",
            },
            night: {
              description: "Thunderstorm",
              image: "http://openweathermap.org/img/wn/11n@2x.png",
            },
          },
          96: {
            day: {
              description: "Thunderstorm With Hail",
              image: "http://openweathermap.org/img/wn/11d@2x.png",
            },
            night: {
              description: "Thunderstorm With Hail",
              image: "http://openweathermap.org/img/wn/11n@2x.png",
            },
          },
          99: {
            day: {
              description: "Thunderstorm With Hail",
              image: "http://openweathermap.org/img/wn/11d@2x.png",
            },
            night: {
              description: "Thunderstorm With Hail",
              image: "http://openweathermap.org/img/wn/11n@2x.png",
            },
          },
        },
      ],
      currentWeather: {},
      formattedWeather: {},
      forecast: {},
    };
  },
  methods: {
    getWeather() {
      axios
        .get(
          "https://api.open-meteo.com/v1/jma?latitude=35.6895&longitude=139.6917&hourly=windspeed_10m,is_day&daily=weathercode,temperature_2m_max,precipitation_sum,windspeed_10m_max&current_weather=true&timezone=Asia%2FTokyo"
        )
        .then((res) => {
          this.currentWeather = res.data.current_weather;
          this.formattedWeather = {
            weather:
              this.currentWeather.is_day == 0
                ? this.weatherCodes[0][this.currentWeather.weathercode].night
                : this.weatherCodes[0][this.currentWeather.weathercode].day,
            temperature: `${this.currentWeather.temperature}°c`,
            windSpeed: `${this.currentWeather.windspeed}km/h`,
            windDirection: this.degreesToDirection(
              this.currentWeather.winddirection
            ),
          };
        });
    },
    degreesToDirection(degrees) {
      // Define compass directions and their degree ranges
      const directions = [
        "North",
        "Northeast",
        "East",
        "Southeast",
        "South",
        "Southwest",
        "West",
        "Northwest",
        "North",
      ];
      const degreeRanges = [
        22.5, 67.5, 112.5, 157.5, 202.5, 247.5, 292.5, 337.5, 360,
      ];

      // Ensure degrees are within the range [0, 360]
      degrees = (degrees + 360) % 360;

      // Determine the direction based on degree ranges
      for (let i = 0; i < directions.length; i++) {
        if (degrees < degreeRanges[i]) {
          return directions[i];
        }
      }

      // If degrees are exactly 360, consider it as North
      return "North";
    },
  },
  mounted() {
    this.getWeather();
  },
};
</script>

<style scoped>
.weatherWidget {
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
}
</style>
