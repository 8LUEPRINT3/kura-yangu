# Kura Yangu 🗳️

**Kenya Voter Registration Center Locator**

A privacy-first, mobile-friendly static website that helps Kenyan voters find their nearest IEBC constituency registration office.

## Privacy First

All geolocation processing runs **entirely in your browser** using the Haversine formula. Your GPS coordinates are **never sent to any server**.

## Features

- **GPS Mode** — Use your device location to find the 3 nearest IEBC offices, sorted by distance
- **Browse Mode** — Browse by County → Constituency to find any office
- **Share** — Share office details via Web Share API or clipboard
- **Offline-ready** — Pure HTML/CSS/JS, no external dependencies
- Covers all **290 constituencies** across Kenya's 47 counties

## Data

Office data sourced from IEBC records covering all 47 counties and 290 constituencies including location addresses, landmarks, and coordinates.

## Tech Stack

- Single `index.html` file (~55KB)
- Zero external dependencies
- Vanilla JavaScript (ES6+)
- Mobile-first CSS (375px+)

## Usage

Simply open `index.html` in any modern browser. No server required.

## License

Open source. Verify all data at [iebc.or.ke](https://www.iebc.or.ke) before visiting any office.
