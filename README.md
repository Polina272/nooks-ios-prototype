# Nooks — iOS prototype

An editable React Native / Expo project for a two-sided relocation marketplace. The interface is in English and starts with a registration preview, followed by a study destination questionnaire. The supplied Nooks logo screenshot is used for both the registration screen and app header; the visual palette follows the supplied presentation screenshots.

## Download this shared copy

If this repository contains `nooks-ios-project.zip`, download that file, extract it, and open the extracted `nooks-ios` folder in Visual Studio Code. The archive contains the complete source code and assets. Then follow **Open and run** below.

## Open and run

The folder is ready to open in Visual Studio Code. In its terminal:

```bash
npm install
npm start
```

### See the screen inside Visual Studio Code

1. Open **Terminal → New Terminal** in VS Code.
2. Run `npm run web` and leave that terminal open.
3. Press **Shift+Command+P**, choose **Browser: Open Integrated Browser**, and enter `http://localhost:8081`.

This is the same interface rendered as a web preview inside VS Code. To test native iPhone behaviour, use Expo Go or an iOS development build.

The project uses Expo SDK 54. To preview on an iPhone, use a compatible Expo Go build and follow the terminal instructions. A local iOS Simulator requires Xcode, which is not installed on this Mac. Run `npm run verify` to type-check and bundle the app for iOS without a simulator.

## What works in this prototype

- Client: first-screen registration preview with email, phone, Google and Microsoft choices; ten-step questionnaire covering destination country, city, university, origin country, familiar currency, solo or shared living, rent budget, travel frequency, food and lifestyle. The rent budget is entered in the user's familiar currency and converted to the destination currency for local comparisons. Completing the questionnaire opens a personalised home screen where the user chooses neighbourhood search, Move, first-night kit, Settle or Circle. Neighbourhood ranking, monthly cost breakdown, comparison and local viewing requests remain available from there.
- Rep: request list, accept a demo request and submit a structured viewing report. The client sees the updated status and report in the same running session.
- Any city: choose from a starter catalog or type any country, city and university. A known country prefills its currency; other destinations allow a three-letter currency code. Add neighbourhoods and known rent, bill, fare, commute and tax estimates to compare. London, UK has **illustrative sample data** to demonstrate automatic matching.

All state is in memory. Closing or reloading the app resets the demo. **Registration is a UI preview only:** no account is created, no code is sent by email or SMS, and Google and Microsoft OAuth are not connected. Users enter their rent budget in a familiar currency; the app converts it to the destination currency for matching against local rents. Users can choose any three-letter familiar currency code; the app requests the latest available reference exchange rate from Frankfurter and shows its date. If the rate cannot be loaded, conversion pauses and the budget step asks the user to retry or choose the destination currency. Exchange rates are indicative and may differ from a bank's rate. Prices, travel times and tax assumptions are not live data. A production release needs an identity provider and provider credentials, a global university and transit data source, current rental listings, payments, rep verification, media upload, real-time calling, location-specific Settle content and persistent storage.

## Project layout

- `App.tsx` — screens and connected client/rep demo flow.
- `src/logic.ts` — city-scoped neighbourhood data, monthly cost estimates and ranking.
- `src/ui.tsx` — shared visual components and palette.
- `src/places.ts` — starter country, city and university choices with custom-entry fallback.
- `src/brand.tsx` and `assets/nooks-logo-source.png` — the supplied logo used consistently in the app. `assets/nooks-app-icon.png` is an opaque square adaptation for the installed app icon.
- `src/logic.test.ts` — calculation and city-scoping checks.
- `src/fx.ts` and `src/fx.test.ts` — automatic reference exchange-rate loading and response checks.
