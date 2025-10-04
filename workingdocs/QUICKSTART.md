# ⚡ LuaPop Quick Start Guide

Get your AI chat widget up and running in under 2 minutes!

## 🚀 30-Second Setup

### Step 1: Add the Script
Copy and paste this into your HTML, right before the closing `</body>` tag:

```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id", // Replace with your actual agent ID
    position: "bottom-right",
    theme: "light",
    buttonText: "Chat with AI"
  });
</script>
```

### Step 2: Replace Agent ID
Get your agent ID from the Lua AI dashboard and replace `"your-agent-id"` in the code above.

### Step 3: Test
Refresh your page - you should see a chat button in the bottom-right corner!

---

## 🎯 Common Setups

### Customer Support Widget
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "support-agent-id",
    chatTitle: "Customer Support",
    buttonText: "Need Help?",
    position: "bottom-right",
    theme: "light",
    chatInputPlaceholder: "How can we help you today?"
  });
</script>
```

### Sales Assistant
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "sales-agent-id",
    chatTitle: "Sales Assistant",
    buttonText: "💰 Get Quote",
    buttonColor: "#28a745",
    position: "bottom-right",
    theme: "light"
  });
</script>
```

### Embedded Chat (No Floating Button)
```html
<!-- Create a container for the chat -->
<div id="my-chat" style="width: 400px; height: 600px; border: 1px solid #ddd;"></div>

<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    displayMode: "embedded",
    embeddedDisplayConfig: {
      targetContainerId: "my-chat"
    },
    theme: "light"
  });
</script>
```

---

## 🎨 Quick Customizations

### Change Position
```javascript
position: "bottom-left"   // Left side
position: "top-right"     // Top right
position: "top-left"      // Top left
```

### Change Colors
```javascript
buttonColor: "#ff6b6b"    // Custom button color
theme: "dark"             // Dark theme
```

### Custom Button Text & Icon
```javascript
buttonText: "💬 Chat Now"
buttonIcon: "🤖"          // Emoji or text
```

### Branding
```javascript
chatTitle: "Your Company Support",
chatHeaderSubtitle: {
  visible: true,
  brandName: "Your Company",
  iconUrl: "https://yoursite.com/logo.png"
}
```

---

## 🔧 Testing & Environments

### Use Staging for Testing
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "staging", // Safe for testing
  // ... other config
});
```

### Production Ready
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "production", // Live environment
  // ... other config
});
```

---

## 📱 Framework Integration

### WordPress
Add to your theme's `footer.php` or use a plugin like "Insert Headers and Footers":

```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    position: "bottom-right",
    theme: "light"
  });
</script>
```

### Shopify
Add to your theme's `theme.liquid` file, before `</body>`:

```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    chatTitle: "Shop Assistant",
    buttonText: "🛍️ Shop Help",
    position: "bottom-right"
  });
</script>
```

### React/Next.js
```tsx
// components/ChatWidget.tsx
import { useEffect } from 'react';

export default function ChatWidget() {
  useEffect(() => {
    // Load script
    const script = document.createElement('script');
    script.src = 'https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js';
    script.onload = () => {
      window.LuaPop?.init({
        agentId: "your-agent-id",
        position: "bottom-right",
        theme: "light"
      });
    };
    document.body.appendChild(script);

    return () => {
      // Cleanup
      document.body.removeChild(script);
    };
  }, []);

  return null;
}

// In your main component
import ChatWidget from './components/ChatWidget';

function App() {
  return (
    <div>
      {/* Your app content */}
      <ChatWidget />
    </div>
  );
}
```

### Vue.js
```vue
<template>
  <div>
    <!-- Your app content -->
  </div>
</template>

<script>
export default {
  mounted() {
    const script = document.createElement('script');
    script.src = 'https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js';
    script.onload = () => {
      window.LuaPop?.init({
        agentId: "your-agent-id",
        position: "bottom-right",
        theme: "light"
      });
    };
    document.body.appendChild(script);
  }
};
</script>
```

### Angular
```typescript
// app.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- Your app content -->`
})
export class AppComponent implements OnInit {
  ngOnInit() {
    const script = document.createElement('script');
    script.src = 'https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js';
    script.onload = () => {
      (window as any).LuaPop?.init({
        agentId: "your-agent-id",
        position: "bottom-right",
        theme: "light"
      });
    };
    document.body.appendChild(script);
  }
}
```

---

## 🔍 Troubleshooting

### Widget Not Showing?
1. **Check the console** for JavaScript errors
2. **Verify your agent ID** is correct
3. **Make sure the script loads** after the page DOM is ready

### Button Appears But Chat Won't Open?
1. **Check your internet connection**
2. **Verify the agent ID exists** in your Lua AI dashboard
3. **Try switching to staging environment** for testing

### Styling Issues?
1. **Check for CSS conflicts** using browser dev tools
2. **Try different positions** if the button is hidden
3. **Use custom styles** to override conflicts:

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  popupButtonStyles: {
    zIndex: "9999", // Ensure button appears on top
    position: "fixed"
  }
});
```

---

## 📊 Track Events (Optional)

Monitor chat interactions for analytics:

```html
<script>
  // Listen for chat events
  window.addEventListener('message', function(event) {
    if (event.data && event.data.type === 'LUA_POP_EVENT') {
      console.log('Chat event:', event.data.eventType);
      
      // Send to Google Analytics
      if (typeof gtag !== 'undefined') {
        gtag('event', 'chat_' + event.data.eventType, {
          event_category: 'engagement'
        });
      }
    }
  });

  // Initialize widget
  window.LuaPop.init({
    agentId: "your-agent-id",
    position: "bottom-right",
    theme: "light"
  });
</script>
```

---

## 🎯 Next Steps

### 1. Customize Appearance
- Try different positions and themes
- Add your brand colors and logo
- Customize button text and icons

### 2. Advanced Features
- Enable voice chat: `voiceModeEnabled: true`
- Add custom navigation handlers
- Implement user session tracking

### 3. Monitor Performance
- Set up event tracking
- Monitor chat engagement
- Analyze user interactions

### 4. Scale Your Implementation
- Create different agents for different pages
- Implement A/B testing with different configurations
- Add conditional loading based on user behavior

---

## 📚 Need More Help?

- **Full Documentation**: [README.md](./README.md)
- **API Reference**: [API.md](./API.md)
- **Examples**: [EXAMPLES.md](./EXAMPLES.md)
- **Support**: [support@heylua.ai](mailto:support@heylua.ai)

---

**That's it!** Your AI chat widget should now be live on your website. The setup takes less than 2 minutes, but the possibilities are endless! 🚀
