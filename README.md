# Weather Union MCP Server

A Model Context Protocol (MCP) server that provides weather data and air quality information using the Weather Union API. This server offers real-time weather data for specific coordinates or predefined Indian cities.

## Quick Start

1. **Set up your API key:**
   ```bash
   export WEATHER_UNION_API_KEY='your-api-key-here'
   ```

2. **Run the server:**
   ```bash
   # For MCP clients (default - uses stdin)
   python weatherunion_mcp/server.py
   
   # For testing with HTTP
   python weatherunion_mcp/server.py --http --port 8000
   ```

## Installation

### Prerequisites
- Python 3.11+
- Weather Union API key (X-Zomato-Api-Key)

### Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd weatherunion-mcp
   ```

2. **Install dependencies:**
   ```bash
   pip install fastmcp requests python-dotenv
   ```

3. **Configure your API key:**
   
   **Option 1: Environment Variable**
   ```bash
   export WEATHER_UNION_API_KEY='your-api-key-here'
   ```
   
   **Option 2: .env File**
   ```bash
   echo "WEATHER_UNION_API_KEY=your-api-key-here" > .env
   ```

4. **Run the server:**
   ```bash
   python weatherunion_mcp/server.py
   ```

## Available Tools

The MCP server provides two powerful weather tools:

### 1. `get_current_weather`
Get current weather data for any geographic location using latitude and longitude coordinates.

**Parameters:**
- `latitude` (float): Latitude coordinate (-90 to 90 degrees)
- `longitude` (float): Longitude coordinate (-180 to 180 degrees)

**Returns:**
Comprehensive weather information including temperature, humidity, wind conditions, precipitation, and air quality data.

**Example:**
```
get_current_weather(12.933756, 77.625825)  # Bangalore coordinates
```

### 2. `get_weather_for_city`
Get weather data for major Indian cities using predefined city names.

**Parameters:**
- `city_name` (str): Name of the city (case-insensitive)
- `country_code` (str, optional): Country code (default: "IN")

**Supported Cities:**
- Bangalore, Mumbai, Delhi, Hyderabad, Chennai
- Kolkata, Pune, Ahmedabad, Jaipur, Lucknow

**Example:**
```
get_weather_for_city("bangalore")
get_weather_for_city("Mumbai")
```

## Weather Data Format

The server returns comprehensive weather information in a formatted string:

```
Weather Information (Lat: 12.933756, Lon: 77.625825):

Temperature: 25.68°C
Humidity: 25.81%
Wind Speed: 1.15 km/h
Wind Direction: 331.2°
Rain Intensity: 0 mm/h
Rain Accumulation: 0.4 mm
Air Quality Index (PM 2.5): 84
Air Quality Index (PM 10): 75
```

## Transport Options

### Default: Standard Input (stdin)
Perfect for MCP clients like Claude Desktop:
```bash
python weatherunion_mcp/server.py
```

### HTTP Transport
For testing and development:
```bash
python weatherunion_mcp/server.py --http --port 8000
```

## Configuration

### Environment Variables
- `WEATHER_UNION_API_KEY`: Your Weather Union API key (required)

### Command Line Options
- `--http`: Use HTTP transport instead of stdin
- `--port`: Port for HTTP server (default: 8000, only used with --http)

## Usage with MCP Clients

### Claude Desktop
Add to your Claude Desktop configuration:
```json
{
  "mcpServers": {
    "weather-union": {
      "command": "uvx",
      "args": ["weatherunion-mcp"],
      "env": {
        "WEATHER_UNION_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Other MCP Clients
The server follows standard MCP protocol and works with any compliant MCP client.

## API Key

You need a Weather Union API key (X-Zomato-Api-Key) to use this server. 

- The server validates your API key on startup
- API key must be set as an environment variable
- The server will show clear error messages if the API key is missing or invalid

## Development

### Project Structure
```
weatherunion-mcp/
├── weatherunion_mcp/
│   ├── __init__.py
│   └── server.py          # Main MCP server implementation
├── .env                   # API key configuration (optional)
├── README.md
└── requirements.txt       # Python dependencies
```

### Dependencies
- `fastmcp >= 0.2.0`: MCP server framework
- `requests >= 2.31.0`: HTTP client for API calls
- `python-dotenv`: Environment variable loading

### Testing
1. **Validate setup:**
   ```bash
   python weatherunion_mcp/server.py
   ```
   
2. **Test with HTTP (for debugging):**
   ```bash
   python weatherunion_mcp/server.py --http --port 8000
   ```

The server will:
- Load your API key from environment/`.env` file
- Validate the API key with a test request
- Show available tools and configuration
- Start the appropriate transport

### Error Handling
The server provides clear error messages for:
- Missing API key
- Invalid API key
- Network connection issues
- Invalid coordinates
- Unsupported cities

## Features

- ✅ **Real-time weather data** from Weather Union API
- ✅ **Air quality information** (PM 2.5 and PM 10)
- ✅ **Coordinate-based queries** for any location
- ✅ **Predefined major Indian cities**
- ✅ **MCP protocol compliance** for AI assistant integration
- ✅ **Environment variable configuration**
- ✅ **Multiple transport options** (stdin/HTTP)
- ✅ **Comprehensive error handling**
- ✅ **API key validation**

## Requirements

- Python 3.8+
- Weather Union API key
- Internet connection for API calls

## Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

## License

This project is open source. See the LICENSE file for details.