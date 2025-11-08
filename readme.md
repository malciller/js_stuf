# DioDashboard Frontend

A modern, real-time monitoring dashboard built with vanilla JavaScript, HTML5, and CSS. Displays system metrics, telemetry data, balance information, and log streams through a customizable widget-based interface.

## Features

### Real-time Monitoring
- **Telemetry Metrics**: Gauge, counter, and histogram metrics with automatic updates
- **System Monitoring**: CPU usage, memory statistics, and system health indicators
- **Balance Tracking**: Asset balances and open trading orders
- **Log Streaming**: Real-time log message display with filtering capabilities

### Interactive Dashboard
- **Widget System**: Drag-and-drop widgets with customizable layouts
- **Auto-layout**: Intelligent widget placement and grid management
- **Persistent Configuration**: Dashboard state saved automatically in browser storage
- **Context Menus**: Right-click menus for widget and canvas interactions

### Real-time Connectivity
- **WebSocket Integration**: Live data streaming from backend services
- **Automatic Reconnection**: Robust connection handling with fallback support
- **Multi-stream Support**: Simultaneous monitoring of multiple data streams

## Technology Stack

- **Frontend**: Vanilla JavaScript (ES6+ modules)
- **Styling**: Tailwind CSS with custom dark theme
- **UI Framework**: Custom component system with modern CSS
- **Data Transport**: WebSocket for real-time communication
- **Storage**: Browser localStorage for configuration persistence

## Project Structure

```
/
├── index.html              # Main HTML file with Tailwind config
├── js/
│   ├── main.js            # Application entry point
│   ├── data/
│   │   └── state.js       # Global state and widget registry
│   ├── components/
│   │   ├── canvas.js      # Main canvas component
│   │   ├── widget-menu.js # Widget selection menu
│   │   └── context-menu.js # Right-click context menus
│   ├── views/
│   │   ├── telemetry.js   # Telemetry data rendering
│   │   ├── balance.js     # Balance data rendering
│   │   ├── system.js      # System metrics rendering
│   │   └── log.js         # Log stream rendering
│   ├── widgets/
│   │   ├── base-widget.js # Base widget class
│   │   ├── telemetry-widget.js
│   │   ├── balance-widget.js
│   │   ├── system-widget.js
│   │   └── log-widget.js
│   └── utils/
│       ├── websocket.js   # WebSocket connection management
│       ├── storage.js     # Configuration persistence
│       ├── drag-drop.js   # Drag and drop functionality
│       ├── auto-layout.js # Widget layout algorithms
│       ├── ui.js          # UI utility functions
│       ├── formatting.js  # Data formatting utilities
│       └── metric-discovery.js # Dynamic metric discovery
├── css/
│   ├── main.css           # Global styles
│   ├── components/        # Component-specific styles
│   ├── views/             # View-specific styles
│   └── widgets/           # Widget-specific styles
└── favicon.png           # Application icon
```

## Getting Started

### Prerequisites
- Modern web browser with WebSocket support
- Backend server running on port 9000 (default configuration)

### Installation

1. **Clone or download** the project files to your web server directory

2. **Configure Backend Connection** (optional):
   ```javascript
   // In js/data/state.js
   export const hostname = 'your-backend-host'; // Default: window.location.hostname
   export const port = 9000; // Default: 9000
   ```

3. **Serve the files** using any static web server:
   ```bash
   # Using Python
   python -m http.server 8000

   # Using Node.js
   npx serve .

   # Using PHP
   php -S localhost:8000
   ```

4. **Open** `http://localhost:8000` in your browser

### Backend Requirements

The dashboard expects a WebSocket server providing data streams on these endpoints:
- `ws://hostname:9000/balance`
- `ws://hostname:9000/system`
- `ws://hostname:9000/telemetry`
- `ws://hostname:9000/log`

Data format should be JSON with appropriate fields for each stream type.

## Usage

### Adding Widgets
1. Click the **+** button in the bottom-right corner
2. Select a widget type from the menu
3. Widgets will be automatically placed on the canvas

### Managing Widgets
- **Drag**: Click and drag widget headers to reposition
- **Resize**: Drag the resize handle in the bottom-right corner
- **Remove**: Right-click a widget → "Remove Widget"
- **Clear All**: Click the **X** button to clear all widgets

### Widget Types

#### Telemetry Widgets
- **Gauge Metrics**: Visual gauges for measurement metrics
- **Counter Metrics**: Incremental counters and rates
- **Histogram Metrics**: Distribution charts for timing data
- **Single Metric**: Individual metric display

#### Balance Widgets
- **Asset Balances**: Portfolio and wallet balances
- **Open Orders**: Active trading orders
- **Single Asset**: Focus on specific asset
- **Symbol Orders**: Orders for specific trading pairs

#### System Widgets
- **CPU Metrics**: Processor usage and core information
- **Memory Metrics**: RAM and swap utilization
- **System Metric**: Individual system measurements

#### Log Widgets
- **Log Stream**: Real-time log message display with search and filtering

## Configuration

### Data Streams
Configure available streams in `js/data/state.js`:
```javascript
export const streams = ['balance', 'system', 'telemetry', 'log'];
```

### Widget Registry
Add new widget types by extending the `widgetRegistry` object in `js/data/state.js`:
```javascript
export const widgetRegistry = {
  'your-widget-type': {
    type: 'your-data-type',
    subtype: 'single', // or 'group' or 'stream'
    title: 'Widget Title',
    description: 'Widget description',
    category: 'your-category',
    defaultSize: { width: 6, height: 4 },
    dynamic: false // true for dynamically created widgets
  }
};
```

## Browser Support

- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

## Development

### Code Style
- ES6+ modules with import/export
- Async/await for asynchronous operations
- Class-based component architecture
- CSS custom properties for theming

### Adding New Widgets

1. **Create Widget Class** in `js/widgets/`:
```javascript
export class YourWidget extends BaseWidget {
  constructor(config) {
    super(config);
    // Widget initialization
  }

  render() {
    // Render widget content
  }

  update(data) {
    // Handle data updates
  }
}
```

2. **Register Widget** in `js/data/state.js`

3. **Add Styling** in `css/widgets/`

### Contributing
1. Follow the existing code structure and naming conventions
2. Add appropriate error handling
3. Test across supported browsers
4. Update documentation for new features

## License

This project is part of the DioDashboard monitoring system.
