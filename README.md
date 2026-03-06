# Global Maritime Vessel Tracker

A static web application for tracking maritime vessels worldwide with anomaly detection capabilities.

## Features

### Map Visualization
- Interactive world map using Leaflet.js
- OpenStreetMap base layer with OpenSeaMap maritime overlay
- Real-time vessel positions displayed as markers
- Vessel markers color-coded by type:
  - Cargo ships (green)
  - Tankers (orange)
  - Other vessels (blue)

### Vessel Information
- Click any vessel marker to view detailed information:
  - Vessel name and MMSI number
  - Vessel type
  - Current position (coordinates)
  - Speed over ground (SOG)
  - Heading/Course
  - Last update timestamp

### Location Filters
Quick navigation to strategic waterways:
- Suez Canal
- Strait of Hormuz
- Strait of Malacca
- Panama Canal
- Turkish Straits (Bosphorus & Dardanelles)
- Strait of Gibraltar
- Global View

### Anomaly Detection
The application displays maritime anomalies with visual alerts:
- **Conflict/War Zones** - Military tensions affecting shipping
- **Channel Closures** - Temporary or permanent waterway closures
- **Weather Events** - Severe weather affecting navigation
- **Traffic Congestion** - Heavy vessel density delays

Each anomaly shows:
- Type and severity level
- Description of the event
- Affected area
- Source and last update time

## Data Sources

### Vessel Tracking
The application attempts to connect to AIS (Automatic Identification System) data streams:
- **Primary**: aisstream.io WebSocket API (free tier)
- **Fallback**: Simulated vessel data around key locations

### Anomaly Data
Anomalies are displayed from a curated database of current maritime events affecting global shipping.

## Usage

### Running Locally
Simply open `index.html` in any modern web browser:
```bash
# Option 1: Direct file open
open index.html

# Option 2: Using Python HTTP server
python -m http.server 8000
# Then visit http://localhost:8000

# Option 3: Using Node.js (if http-server is installed)
npx http-server
```

### Deployment

This is a static website that can be deployed to:
- GitHub Pages
- Netlify
- Vercel
- Any static web hosting service

No build process or server-side code required.

### GitHub Pages (Automated)

This repository includes a GitHub Actions workflow (`.github/workflows/deploy.yml`) that automatically deploys to GitHub Pages:

1. **Enable GitHub Pages:**
   - Go to Settings → Pages
   - Under "Build and deployment", select **GitHub Actions** as the source

2. **Push to main branch:**
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

3. **Access your site:**
   - After the workflow completes (check the Actions tab), your site will be available at:
   - `https://YOUR_USERNAME.github.io/REPO_NAME/`

4. **Manual trigger:**
   - You can also manually trigger deployment from the Actions tab → "Deploy to GitHub Pages" → "Run workflow"

### Other Platforms

## Technical Details

### Dependencies
All loaded via CDN (no installation required):
- Leaflet.js 1.9.4 (map library)
- Font Awesome 6.4.0 (icons)
- OpenStreetMap tiles
- OpenSeaMap tiles (maritime markers)

### Architecture
- Single HTML file with embedded CSS and JavaScript
- WebSocket connection for real-time AIS data
- Client-side rendering of map and markers
- Simulated data fallback when API unavailable

### Browser Support
- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Mobile browsers (iOS Safari, Chrome Mobile)

## API Configuration

### AIS Stream API
To use real vessel data instead of simulations:

1. Visit https://aisstream.io and create a free account
2. Obtain your API key
3. Replace `TEST_KEY` in the JavaScript with your actual API key:
   ```javascript
   const subscription = {
       APIKey: "YOUR_ACTUAL_API_KEY",
       BoundingBoxes: [[[-90, -180], [90, 180]]]
   };
   ```

### Alternative Data Sources
The application can be modified to work with:
- MarineTraffic API
- VesselFinder API
- VesselAPI
- Custom AIS receivers

## Customization

### Adding New Anomalies
Edit the `anomalies` array in the JavaScript section:
```javascript
const anomalies = [
    {
        id: 'anomaly-5',
        lat: 0.0000,
        lng: 0.0000,
        title: 'Your Anomaly Title',
        type: 'conflict', // or 'closure', 'weather', 'traffic'
        severity: 'high', // or 'medium', 'low'
        description: 'Description here...',
        affectedArea: 'Area description',
        lastUpdated: new Date().toISOString(),
        source: 'Your Source'
    }
];
```

### Adding New Locations
Edit the `locations` object:
```javascript
newlocation: { 
    name: 'Location Name', 
    lat: 0.0000, 
    lng: 0.0000, 
    zoom: 10,
    bounds: [[lat1, lng1], [lat2, lng2]]
}
```

## License

This project is open source and available for educational and commercial use.

## Notes

- The application uses simulated vessel data when real AIS data is unavailable
- Anomaly data should be updated regularly for accuracy
- For production use, obtain a valid AIS data API key
- Respect rate limits and terms of service for all APIs used
