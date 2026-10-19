# Stock Market App

An Android app built with Kotlin and Jetpack Compose for browsing listed companies and viewing intraday stock prices. Company listings and price data come from the Alpha Vantage API as CSV, are parsed in the app, and the listings are cached in a local Room database.

<!--
Screenshots: add the company list and a company info screen with its chart, for example:
<p float="left">
  <img src="screenshots/listings.png" width="220" />
  <img src="screenshots/company_info.png" width="220" />
</p>
-->

## Features

- Company listings with search, served from a Room cache and refreshed from the network
- Pull to refresh on the listings screen
- Company info screen with the company profile and an intraday price chart drawn on a Compose Canvas
- CSV parsing with OpenCSV for both the listings and the intraday data
- Mappers between DTOs, Room entities and domain models

## Tech stack

| Area | Tools |
|---|---|
| UI | Jetpack Compose, Material 3, Material icons, Accompanist SwipeRefresh |
| Architecture | Clean Architecture, MVVM |
| Dependency injection | Hilt |
| Networking | Retrofit, Moshi, OkHttp logging interceptor |
| Local data | Room |
| Parsing | OpenCSV |
| Async | Kotlin Coroutines and Flow |

## Architecture

```
com.mosab.stockmarket/
├── data/
│   ├── remote/        # StockApi (Alpha Vantage) and DTOs
│   ├── csv/           # CSVParser interface, listings and intraday parsers
│   ├── local/         # Room database, DAO, entities
│   ├── mapper/        # DTO, entity and domain mappers
│   └── repository/    # StockRepositoryImpl (cache first, then network)
├── domain/
│   ├── model/         # CompanyListing, CompanyInfo, IntradayInfo
│   └── repository/    # StockRepository contract
├── presentation/
│   ├── companylistings/  # screen, ViewModel, events, state
│   └── companyinfo/      # screen, ViewModel, state, StockChart
└── di/                # Hilt modules
```

## Getting started

1. Get a free API key from [Alpha Vantage](https://www.alphavantage.co/support/#api-key).
2. Put your key in `StockApi.API_KEY` (`data/remote/StockApi.kt`).
3. Open the project in Android Studio, sync Gradle and run the `app` configuration (API 24 or newer).
