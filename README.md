# Weather Dashboard (React)

Assignment 5: the Weather Dashboard from Assignment 4, rebuilt as a React app with Vite.

It uses the free [Open-Meteo](https://open-meteo.com/) API, so **no API key is needed**.

## How to run

You need [Node.js](https://nodejs.org/) (version 18 or newer).

```bash
npm install
npm run dev
```

Then open the link shown in the terminal (usually http://localhost:5173).

## Project structure

```
src/
  main.jsx                  Entry point, mounts <App />
  App.jsx                   Holds the state and fetches the weather (useEffect)
  index.css                 Styles
  api/weather.js            Fetch calls to Open-Meteo (geocoding + forecast)
  utils/weather.js          Weather code descriptions and formatting helpers
  components/
    SearchBar.jsx           City input and search button
    LoadingSpinner.jsx      Shown while a request is in progress
    ErrorMessage.jsx        Shown when the city is not found or the request fails
    WeatherCard.jsx         Shows the current weather of the city
    WeatherIcon.jsx         SVG icon for the weather condition
    DetailItem.jsx          One small box (feels like, humidity, wind, rain chance)
```

## State and props

- `App` has the main state with `useState`: `city`, `weather`, `isLoading` and `error`.
- `SearchBar` has its own `query` state for the text in the input. It only sends the
  city up to `App` (with the `onSearch` prop) when the form is submitted.
- A `useEffect` in `App` runs when `city` changes and fetches the weather. Its
  dependency array is `[city]`. The cleanup function ignores an old response if the user
  searches for another city before the first request is done.
- `App` shows `LoadingSpinner`, `ErrorMessage` or `WeatherCard` depending on the state.

Props go at most two levels deep: `App` → `WeatherCard` → `WeatherIcon` / `DetailItem`.
The state lives in `App` because it is the common parent of the search bar and the
results, so no extra state management (like Context) was needed.
