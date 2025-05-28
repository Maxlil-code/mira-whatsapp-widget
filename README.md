# Mira.AI WhatsApp Widget

A customizable WhatsApp widget for easy integration with Mira.AI services.

## Usage

### Via jsDelivr CDN

```html
<script>
    window.MiraWidgetConfig = {
        whatsappMessage: "Optional default message",
        titleText: "Your Title",
        subText: "Your Subtitle",
    };
</script>
<script src="https://cdn.jsdelivr.net/gh/mira-ai/widget@latest/dist/mira-widget.min.js"></script>
```

## CMS Integration

### WordPress
```php
// Add to your theme's footer.php or via a plugin
<script>
window.MiraWidgetConfig = {
    whatsappMessage: "Hi from WordPress!",
    titleText: "Need help?",
    subText: "Chat with Mira.AI"
};
</script>
<script src="https://cdn.jsdelivr.net/gh/mira-ai/widget@latest/dist/mira-widget.min.js"></script>
```

### Shopify
```liquid
<!-- Add to theme.liquid -->
{% raw %}
<script>
window.MiraWidgetConfig = {
    whatsappMessage: "Question about {{product.title}}",
    titleText: "Need assistance?",
    subText: "Chat with our AI assistant"
};
</script>
{% endraw %}
<script src="https://cdn.jsdelivr.net/gh/mira-ai/widget@latest/dist/mira-widget.min.js"></script>
```

### Other Platforms
The widget works with any platform that can add custom HTML/JavaScript:
- Wix
- Squarespace
- Webflow
- React/Vue/Angular apps
- Static HTML sites

### Configuration Options

- `whatsappMessage`: Pre-filled message (optional)
- `titleText`: Widget title text (required)
- `subText`: Widget subtitle text (required)

## Development

1. Clone the repository
2. Install dependencies: `npm install`
3. Build: `npm run build`

## License

MIT
