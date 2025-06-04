# Mira.AI WhatsApp Widget

A **drop‑in, zero‑dependency widget** that lets your visitors open a WhatsApp chat or scan a QR‑code straight from any page. It works everywhere you can add a `<script>` tag—static HTML, WordPress, Shopify, React, Vue, Angular… you name it.

---

## 1  Quick Start (CDN)

```html
<!-- 1️⃣  Add global config BEFORE the widget script -->
<script>
  window.MiraWidgetConfig = {
    whatsappMessage: "Hi! I'm interested in your services ✨", // optional
    titleText       : "Need Help?",                           // required
    subText         : "Chat with Mira.AI",                    // required
    // containerId : "custom‑placeholder"                     // optional (see §3)
  };
</script>

<!-- 2️⃣  Load the widget -->
<script src="https://cdn.jsdelivr.net/gh/mira‑ai/widget@latest/dist/mira-widget.min.js"></script>
```

> **That’s it.** A floating button appears in the bottom‑right corner by default. Clicking it reveals the QR code + deep‑link to WhatsApp.

---

## 2  Configuration Reference

| Property          | Type   | Default          | Description                                                                                                                 |
| ----------------- | ------ | ---------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `titleText`       | string | — (**required**) | Title shown on the button.                                                                                                  |
| `subText`         | string | — (**required**) | Subtitle under the title.                                                                                                   |
| `whatsappMessage` | string | `""`             | Prefilled text in the WhatsApp chat.                                                                                        |
| `position`        | string | `"bottom-right"` | One of `bottom-right`, `bottom-left`, `top-right`, `top-left` (only used in **floating** mode).                             |
| `containerId`     | string | *(none)*         | **Embed** mode: ID of the element where the widget should be rendered. If omitted the widget floats and follows `position`. |

---

## 3  Embed vs Floating Mode

### Floating (default)

No `containerId` ⇒ the widget is `position:fixed` to the viewport.

### Embedded inside any element

```html
<div id="promo‑spot"></div>
<script>
  window.MiraWidgetConfig = {
    titleText : "Apply now!",
    subText   : "Via WhatsApp",
    containerId: "promo‑spot" // 🔗 render RIGHT HERE
  };
</script>
<script src="https://cdn.jsdelivr.net/gh/mira‑ai/widget@latest/dist/mira-widget.min.js"></script>
```

The dropdown will align itself neatly above the trigger button when the container is near the bottom of the viewport, and below it when near the top.

---

## 4  CMS Recipes

### WordPress (theme or plugin)

```php
<!-- footer.php -->
<script>
  window.MiraWidgetConfig = {
    titleText : "Need advice?",
    subText   : "Talk to Mira.AI",
    whatsappMessage: "Hi, I found you via our website!",
  };
</script>
<script src="https://cdn.jsdelivr.net/gh/mira‑ai/widget@latest/dist/mira-widget.min.js"></script>
```

### Shopify

```liquid
<!-- theme.liquid, before </body> -->
{% raw %}
<script>
  window.MiraWidgetConfig = {
    titleText : "Questions?",
    subText   : "Chat with us on WhatsApp",
    whatsappMessage: "Hi! I’m looking at {{ product.title }}",
  };
</script>
{% endraw %}
<script src="https://cdn.jsdelivr.net/gh/mira‑ai/widget@latest/dist/mira-widget.min.js"></script>
```

### Wix / Squarespace / Webflow

Just paste the same two `<script>` tags into your **Custom Code / Footer HTML** section.

---

## 5  Frontend Frameworks

> The widget is plain IIFE JavaScript: no React, Vue or Angular bindings needed. Load it **once** per page, preferably in \`\` (the HTML template) so every route has access.

### React (Vite / CRA)

```html
<!-- public/index.html -->
<body>
  <div id="root"></div>
  <script>
    window.MiraWidgetConfig = {
      titleText : "Need help?",
      subText   : "Chat with Mira.AI",
    };
  </script>
  <script src="https://cdn.jsdelivr.net/gh/mira‑ai/widget@latest/dist/mira-widget.min.js"></script>
</body>
```

### Vue + Vite / Nuxt (client‑side)

Add the two tags to `index.html` (Vue) or `app.vue` (`<template>` → `<head>` via Nuxt’s `<Head>` component).

### Angular

Insert the tags in `src/index.html` right before `</body>`.

The widget is global—no need to import anything in your TS code.

---

## 6  Advanced API (runtime control)

Once loaded, a global object \`\` becomes available:

```js
window.MiraCustomWidget.open();   // programmatically open
window.MiraCustomWidget.close();  // close
window.MiraCustomWidget.toggle(); // toggle state
window.MiraCustomWidget.remove(); // completely remove from the DOM
```

---

## 7  Troubleshooting

| Symptom             | Cause / Fix                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------- |
| Widget doesn’t show | Make sure **both** `<script>` tags are present *and* `titleText`/`subText` are provided.          |
| Wrong container ID  | The widget logs `Container with id "…" not found` in the console and falls back to floating mode. |
| Multiple widgets    | The script guards against duplicates: only the **first** instance on the page will render.        |

---

## 8  Development & Build

```bash
# Clone
$ git clone https://github.com/mira-ai/widget.git && cd widget

# Install dependencies (only for local development tools)
$ npm install

# Build minified bundle into /dist
$ npm run build
```

`/dist/mira-widget.min.js` is what gets published to jsDelivr.

---

## 9  Contributing

Pull requests are welcome! Please open an issue first to discuss any big change.

---

## 10  License

[MIT](LICENSE)

---

**Happy chatting 👋**
