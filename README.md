# SafeChat Checker Prototype 🛡️

## Demo Link

Try the live prototype here:  
[https://frr-drj.github.io/SafeChat-Checker-Prototype/](https://frr-drj.github.io/SafeChat-Checker-Prototype/)

## Project Overview

SafeChat Checker is a **prototype web application** designed to detect scam messages, suspicious links, phone numbers, and Gmail addresses in user-submitted text. It provides an intuitive user interface with dark mode, message history, and real-time risk assessment, simulating an actual backend scanning service.

This project acts as a **foundation and demonstration** of how a scam detection system can operate with a **replaceable backend scanning API**, enabling developers to integrate more complex algorithms, authentication checks, and verification services in the future.

---

## Key Features

- **User-friendly Interface:** Clean and responsive UI with support for dark mode, making it comfortable to use in different lighting conditions.
- **Flexible Input:** Accepts free-text input including scam messages, suspicious URLs, phone numbers, and Gmail addresses for scanning.
- **Mock Backend API Simulation:** Uses an asynchronous mock backend function to simulate scanning and risk evaluation, which can easily be replaced by real backend API calls.
- **Detailed Risk Assessment:** Displays risk levels (Safe, Suspicious, Dangerous) with detected suspicious phrases, URLs, emails, and phone numbers.
- **Local History Storage:** Maintains a history of last 10 checked messages stored in localStorage for quick access and re-checking.
- **Copyable Results:** Allows users to copy scan results easily for sharing or reporting purposes.

---

## Purpose and Usage

The prototype is built to demonstrate the workflow between the frontend and a backend scam detection service. It focuses on:

- Separating frontend UI concerns from backend logic
- Simulating asynchronous scanning calls that return JSON-formatted reports
- Rendering results in a user-friendly and informative manner
- Providing hooks to replace the mock backend with real services without changing the UI or flow

---

## Developer Notes: Extensibility and Backend Integration

### Replaceable Backend API

The core scanning logic resides in the `mockBackendScanAPI` JavaScript function. This function:

- Simulates network latency with asynchronous delay
- Analyzes the input text for predefined scam indicators
- Returns a structured JSON object containing:
  - Risk level and risk score
  - Detected suspicious phrases, URLs, emails, phone numbers
  - Actionable advice based on risk level

### How to Replace with Real Backend

To integrate an actual backend, replace `mockBackendScanAPI` with your real API call, typically using `fetch` or other HTTP client libraries:

```js
async function realBackendScanAPI(message) {
  const response = await fetch("https://yourapi.example.com/scan", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ message }),
  });
  if (!response.ok) throw new Error("API error");
  return await response.json();
}
