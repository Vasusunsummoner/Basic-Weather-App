# Basic-Weather-App

import requests

def get_weather(api_key, location):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        'q': location,
        'appid': api_key,
        'units': 'metric'  # You can change this to 'imperial' for Fahrenheit
    }

    try:
        response = requests.get(base_url, params=params)
        data = response.json()

        if response.status_code == 200:
            return data
        else:
            print(f"Error: {data['message']}")
            return None

    except Exception as e:
        print(f"An error occurred: {e}")
        return None

def display_weather(weather_data):
    if weather_data:
        print("\nCurrent Weather:")
        print(f"Temperature: {weather_data['main']['temp']}°C")
        print(f"Humidity: {weather_data['main']['humidity']}%")
        print(f"Weather: {weather_data['weather'][0]['description']}")
    else:
        print("Unable to fetch weather data.")

if __name__ == "__main__":
    api_key = "0f91677545aca7b6b83402dbeb2c5228"
    location = input("Enter city or ZIP code: ")

    weather_data = get_weather(api_key, location)

    display_weather(weather_data)
