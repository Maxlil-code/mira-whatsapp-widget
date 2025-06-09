# Mira.AI WhatsApp Widget

A **drop‑in, zero‑dependency widget** that lets your visitors open a WhatsApp chat or scan a QR‑code straight from any page. It works everywhere you can add a `<script>` tag—static HTML, WordPress, Shopify, React, Vue, Angular… you name it.

---

## 1  Quick Start (CDN)

```html
<!-- 1️⃣  Add global config BEFORE the widget script -->
<script>
  window.MiraWidgetConfig = {
    whatsappMessage: "Hi Mira! I'm interested in your services ✨. I was refered by {referal code}", // optional
    titleText       : "Applying from outside Germany?",       // required
    subText         : "Chat with Mira.AI",                    // required
    // containerId : "custom‑placeholder"                     // optional (see §3)
  };
</script>

<!-- 2️⃣  Load the widget -->
<script src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"></script>
```

> **That's it.** A floating button appears in the bottom‑right corner by default. Clicking it reveals the QR code + deep‑link to WhatsApp.

---

## 2  Configuration Reference

| Property          | Type   | Default          | Description                                                                                                                 |
| ----------------- | ------ | ---------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `titleText`       | string | — (**required**) | Title shown on the button.                                                                                                  |
| `subText`         | string | — (**required**) | Subtitle under the title.                                                                                                   |
| `whatsappMessage` | string | `""`             | Prefilled text in the WhatsApp chat.                                                                                        |
| `position`        | string | `"bottom-right"` | One of `bottom-right`, `bottom-left`, `top-right`, `top-left` (only used in **floating** mode).                             |
| `containerId`     | string | *(none)*         | **Embed** mode: ID of the element where the widget should be rendered. If omitted the widget floats and follows `position`. |

---

## 3  Embed vs Floating Mode

### Floating (default)

No `containerId` ⇒ the widget is `position:fixed` to the viewport.

### Embedded inside any element

```html
<div id="promo‑spot" style="height: 400px; width: 300px;"></div>
<script>
  window.MiraWidgetConfig = {
    whatsappMessage: "Hi Mira! I'm interested in your services ✨. I was refered by {referal code}",
    titleText : "Applying from outside Germany?",       // required
    subText : "Chat with Mira.AI",  
    containerId: "promo‑spot" // 🔗 render RIGHT HERE
  };
</script>
<script src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"></script>
```

> **Note:** Embedded widgets have a default width of **250px** and will take the full height of their container.

---

## 4  CMS Recipes

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
<script src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"></script>
```

### Shopify

```liquid
<!-- theme.liquid, before </body> -->
{% raw %}
<script>
  window.MiraWidgetConfig = {
    titleText : "Questions?",
    subText   : "Chat with us on WhatsApp",
    whatsappMessage: "Hi Mira!",
  };
</script>
{% endraw %}
<script src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"></script>
```

### Wix / Squarespace / Webflow

Just paste the same two `<script>` tags into your **Custom Code / Footer HTML** section.

---

## 5  Frontend Frameworks

> The widget is plain IIFE JavaScript: no React, Vue or Angular bindings needed. Load it **once** per page, preferably in the HTML template so every route has access.

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
  <script src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"></script>
</body>
```

### Next.js

```typescript
// app/layout.tsx or pages/_app.tsx
import Script from 'next/script'

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {children}
        <Script id="mira-widget-config" strategy="beforeInteractive">
          {`
            window.MiraWidgetConfig = {
              titleText: "Need help?",
              subText: "Chat with Mira.AI",
              whatsappMessage: "Hi! I'm interested in your services ✨"
            };
          `}
        </Script>
        <Script
          src="https://cdn.jsdelivr.net/gh/useconsul/mira-whatsapp-widget@latest/dist/mira-widget.min.js"
          strategy="afterInteractive"
        />
      </body>
    </html>
  )
}
```

### Vue + Vite / Nuxt (client‑side)

Add the two tags to `index.html` (Vue) or `app.vue` (`<template>` → `<head>` via Nuxt's `<Head>` component).

### Angular

Insert the tags in `src/index.html` right before `</body>`.

The widget is global—no need to import anything in your TS code.

---

## 6  Advanced API (runtime control)

Once loaded, a global object becomes available:

```js
window.MiraCustomWidget.open();   // programmatically open
window.MiraCustomWidget.close();  // close
window.MiraCustomWidget.toggle(); // toggle state
window.MiraCustomWidget.remove(); // completely remove from the DOM
```

---

## 7  Troubleshooting

| Symptom             | Cause / Fix                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------- |
| Widget doesn't show | Make sure **both** `<script>` tags are present *and* `titleText`/`subText` are provided.          |
| Wrong container ID  | The widget logs `Container with id "…" not found` in the console and falls back to floating mode. |
| Multiple widgets    | The script guards against duplicates: only the **first** instance on the page will render.        |

---

## 8  License

[MIT](LICENSE)

