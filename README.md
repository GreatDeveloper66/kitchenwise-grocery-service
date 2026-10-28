# kitchenwise-grocery-service

A microservice that discovers nearby grocery stores based on a user's location and search radius using the Google Places API. Part of the KitchenWise application — a full-stack microservice architecture for personalized meal planning and local grocery store discovery.

---

## Overview

This service accepts a geographic coordinate and search radius, then queries the Google Places API to return a structured list of nearby grocery stores. Each result includes store details such as name, address, hours of operation, ratings, and contact information — giving users everything they need to plan a shopping trip around their generated meal plan.

---

## Tech Stack

- **Runtime:** Node.js
- **Language:** TypeScript
- **Framework:** Express
- **External API:** Google Places API

---

## Features

- Finds grocery stores within a configurable radius from a given location
- Returns rich store data including hours, address, ratings, and contact info
- Real-time open/closed status per store
- Structured weekly hours and next open time

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/stores/nearby` | Find grocery stores near a given location and radius |

---

## Request Schema

```typescript
{
  location: {
    latitude: number
    longitude: number
  }
  radius: number  // in meters
}
```

## Response Schema

```typescript
{
  stores: [
    {
      placeId: string
      name: string
      formattedAddress: string
      phoneNumber: string
      rating: number
      userRatingCount: number
      businessStatus: string
      regularOpeningHours: {
        openNow: boolean
        weekdayDescriptions: string[]
        nextOpenTime: string
      }
      hoursStatus: {
        isOpen: boolean
        message: string
        hoursUntilOpen: number
        nextOpenTime: string
      }
    }
  ]
}
```

---

## Environment Variables

Create a `.env` file in the root of the project with the following variables:

```env
PORT=3005
GOOGLE_PLACES_API_KEY=your_google_places_api_key
JWT_SECRET=your_jwt_secret
```

---

## Getting Started

### Prerequisites
- Node.js v18+
- Google Places API key with Places API enabled

### Installation

```bash
git clone https://github.com/GreatDeveloper66/kitchenwise-grocery-service.git
cd kitchenwise-grocery-service
npm install
```

### Development

```bash
npm run dev
```

### Production

```bash
npm run build
npm start
```

---

## Known Limitations

- Store photo retrieval is currently in development
- Results are limited to grocery store category types

---

## Project Architecture

This repository is one of seven components in the KitchenWise application (six backend microservices plus the React frontend):

| Repository | Responsibility |
|---------|---------------|
| [kitchenwise-frontend](https://github.com/GreatDeveloper66/kitchenwise-frontend) | React + TypeScript frontend |
| [user-auth-service](https://github.com/GreatDeveloper66/user-auth-service) | Authentication & JWT management |
| [kitchenwise-diet-profile-service](https://github.com/GreatDeveloper66/kitchenwise-diet-profile-service) | Diet profile storage & management |
| [kitchenwise-meal-plan-service](https://github.com/GreatDeveloper66/kitchenwise-meal-plan-service) | AI-powered meal plan generation |
| [kitchenwise-plan-storage-service](https://github.com/GreatDeveloper66/kitchenwise-plan-storage-service) | User meal plan storage |
| **[kitchenwise-grocery-service](https://github.com/GreatDeveloper66/kitchenwise-grocery-service)** | Grocery store discovery by location (Google Places) |
| [kitchenwise-recipe-service](https://github.com/GreatDeveloper66/kitchenwise-recipe-service) | AI recipe generation |
