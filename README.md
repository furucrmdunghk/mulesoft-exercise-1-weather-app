# How The Weather Today

A MuleSoft 4 application that provides weather information for multiple cities using the OpenWeatherMap API.

## 📋 Description

This Mule application exposes a REST API endpoint that accepts one or more city names and returns current weather information including temperature (min/max) and humidity for each city.

## 🚀 Features

- **Multi-city Support**: Query weather for multiple cities in a single request
- **Temperature Conversion**: Automatically converts temperature from Kelvin to Celsius
- **RESTful API**: Simple HTTP endpoint for easy integration
- **Error Handling**: Validates city input and handles empty values
- **Detailed Logging**: Comprehensive logging at each processing step

## 🛠️ Technical Stack

- **Mule Runtime**: 4.10.1
- **Java**: 17
- **Maven**: Build and dependency management
- **Connectors**:
  - HTTP Connector 1.11.0
  - Sockets Connector 1.2.7
- **External API**: OpenWeatherMap API

## 📁 Project Structure

```
howtheweathertoday/
├── src/
│   ├── main/
│   │   ├── mule/
│   │   │   └── howtheweathertoday.xml    # Main Mule flow
│   │   └── resources/
│   │       ├── weather.properties        # API configuration
│   │       └── log4j2.xml               # Logging configuration
│   └── test/
│       ├── munit/                       # MUnit test files
│       └── resources/
├── pom.xml                              # Maven configuration
└── mule-artifact.json                   # Mule artifact metadata
```

## ⚙️ Configuration

### Prerequisites

1. **Anypoint Studio** 7.x or later
2. **JDK 17**
3. **Maven 3.6+**
4. **OpenWeatherMap API Key** (get one at https://openweathermap.org/api)

### Setup

1. Clone or download this project
2. Update the `src/main/resources/weather.properties` file with your OpenWeatherMap API key:
   ```properties
   weather.api.baseUrl=https://api.openweathermap.org/data/2.5/weather
   weather.api.appid=YOUR_API_KEY_HERE
   ```

## 🎯 API Usage

### Endpoint

```
POST http://localhost:8081/weather
Content-Type: application/json
```

### Request Format

```json
{
  "city": "Hanoi,Tokyo,London"
}
```

**Note**: Cities should be comma-separated in a single string.

### Response Format

```json
[
  {
    "City": "Hanoi",
    "MinTemp": 18.5,
    "MaxTemp": 25.3,
    "Humidity": 75
  },
  {
    "City": "Tokyo",
    "MinTemp": 12.1,
    "MaxTemp": 16.8,
    "Humidity": 62
  },
  {
    "City": "London",
    "MinTemp": 8.2,
    "MaxTemp": 11.5,
    "Humidity": 81
  }
]
```

### Response Fields

- **City**: City name
- **MinTemp**: Minimum temperature in Celsius
- **MaxTemp**: Maximum temperature in Celsius
- **Humidity**: Humidity percentage

## 🏃 Running the Application

### Using Anypoint Studio

1. Import the project into Anypoint Studio
2. Right-click on the project → Run As → Mule Application
3. Wait for the application to start
4. The API will be available at `http://localhost:8081/weather`

### Using Maven

```bash
# Clean and install
mvn clean install

# Run the application
mvn mule:run
```

## 🧪 Testing

### Using cURL

```bash
curl -X POST http://localhost:8081/weather \
  -H "Content-Type: application/json" \
  -d '{"city": "Hanoi,Tokyo,London"}'
```

### Using Postman

1. Create a new POST request to `http://localhost:8081/weather`
2. Set Content-Type header to `application/json`
3. Add request body:
   ```json
   {
     "city": "Hanoi,Tokyo,London"
   }
   ```
4. Send the request

## 🔧 Flow Description

The application implements the following flow:

1. **HTTP Listener**: Receives POST requests on `/weather` endpoint
2. **Input Logging**: Logs the incoming payload
3. **City Splitting**: Parses comma-separated city names
4. **For Each Loop**: Iterates through each city
   - Validates city name is not empty
   - Calls OpenWeatherMap API for each city
   - Collects response data
5. **Response Formatting**: Transforms raw API response to simplified JSON format with temperature conversion (Kelvin to Celsius)
6. **Response**: Returns formatted weather data as JSON array

## 📊 Logging

The application includes comprehensive logging at multiple levels:

- Input payload logging
- City name parsing
- Individual API request logging
- Response transformation logging
- Final payload logging

Logs can be found in the console output or log files as configured in `log4j2.xml`.

## 🔐 Security Considerations

- **API Key Management**: Store API keys securely using encrypted properties or environment variables in production
- **Rate Limiting**: Consider implementing rate limiting to prevent API quota exhaustion
- **Input Validation**: The app validates city inputs, but additional validation may be needed for production use

## 📝 Future Enhancements

- [ ] Add caching mechanism to reduce API calls
- [ ] Implement error handling for invalid city names
- [ ] Add support for additional weather parameters (wind speed, pressure, etc.)
- [ ] Add unit tests using MUnit
- [ ] Add API documentation using RAML
- [ ] Implement circuit breaker pattern for API resilience
- [ ] Add support for different temperature units (Fahrenheit, Kelvin)

## 🐛 Troubleshooting

### Common Issues

1. **Connection Refused**
   - Ensure the application is running
   - Check if port 8081 is available
   - Verify firewall settings

2. **Invalid API Key**
   - Verify your OpenWeatherMap API key is valid
   - Check the `weather.properties` file configuration

3. **Empty Response**
   - Check if city names are spelled correctly
   - Verify internet connectivity
   - Check OpenWeatherMap API status

## 📄 License

This project is created for educational and demonstration purposes.

## 👥 Author

DUNGHK

## 📞 Support

For issues or questions, please refer to:
- [MuleSoft Documentation](https://docs.mulesoft.com/)
- [OpenWeatherMap API Documentation](https://openweathermap.org/api)

---

**Version**: 1.0.0-SNAPSHOT  
**Last Updated**: February 2026
