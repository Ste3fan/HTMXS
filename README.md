
# HTMXS

HTMXS is a lightweight client-side companion script designed to work directly with htmx. It provides targeted micro-updates, DOM morphing, script execution within out-of-band partials, stream resilience for real-time events, and a simple bridge for native browser and device APIs.

## Acknowledgements and Credits

HTMXS is built on top of the concepts and architecture created by the htmx project.

We would like to express our gratitude and appreciation to Carson Gross and the htmx community (https://htmx.org) for creating such a practical, reliable, and elegant approach to modern web development. Their work made it possible to build rich, interactive web applications without the overhead of heavy JavaScript frameworks.

## What HTMXS Adds

While htmx handles request lifecycle and standard DOM swaps, HTMXS introduces several specialized features for server-driven interfaces:

1. Targeted Micro-Updates: Apply atomic changes such as adding or removing CSS classes, or updating single attributes on existing DOM elements without having to replace whole containers.
2. DOM Morphing: Morph existing elements into new structures while preserving active input focus, text selection, and form state during partial page re-renders.
3. Out-of-Band Script Execution: Automatically evaluate scripts located inside dynamically swapped out-of-band fragments.
4. Stream Reconnection: Built-in ping, health check, and reconnection logic for Server-Sent Events (SSE) and WebSocket connections.
5. Dynamic Asset Loading: Load stylesheets and scripts on demand when new UI components appear on the page.
6. Native Device Bridge: A unified interface to interact with modern browser APIs including clipboard, geolocation, battery status, haptic vibration, speech synthesis, screen wake lock, motion sensors, and QR camera scanning.

## Quick Start

Include htmx first, then include HTMXS right after it in your HTML document:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTMXS Application</title>
    <!-- 1. Include htmx -->
    <script src="https://unpkg.com/htmx.org@2.0.0"></script>
    <!-- 2. Include HTMXS -->
    <script src="htmxs.min.js"></script>
</head>
<body>
    <div id="content">
        <!-- Your server-rendered application -->
    </div>
</body>
</html>
```

## Basic Usage

### 1. Granular Attribute and Class Updates

HTMXS listens to custom response headers or micro-attributes to modify existing elements directly:

```html
<!-- Example of a micro-update fragment returned from server -->
<div id="status-badge" htmxs-add-class="is-active" htmxs-remove-class="is-pending"></div>
```

### 2. DOM Morphing

To use the morphing algorithm on a swap target, specify the morph update mode:

```html
<button hx-post="/update-data"
        hx-target="#data-table"
        htmxs-update="morph">
    Refresh Data
</button>
```

### 3. Checking Version from Browser Console

You can inspect the loaded version at any time directly in the browser developer console:

```javascript
htmxs.getVersion();
// Returns: "3.0"

htmxs.printVersion();
// Prints: HTMXS Version 3.0
```

## Device APIs (FoxyDeviceBridge)

HTMXS exposes helper methods on window.FoxyDeviceBridge for applications that need hardware and device capabilities:

```javascript
// Copy text to clipboard
FoxyDeviceBridge.copyToClipboard("Text to copy");

// Trigger haptic vibration on supported devices
FoxyDeviceBridge.vibrate([100, 50, 100]);

// Read geolocation coordinates
FoxyDeviceBridge.getCurrentPosition();

// Speak text using speech synthesis
FoxyDeviceBridge.speak("Document saved successfully", "en-US");
```

## File Structure

- htmxs.js - Full source code with inline comments
- htmxs.min.js - Production minified build
- description.txt - Short project summary

