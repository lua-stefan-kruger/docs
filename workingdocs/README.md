# 🎯 LuaPop - Embeddable AI Chat Widget

LuaPop is a powerful, embeddable chat widget that brings AI-powered conversations directly to your website. Similar to Intercom or Zendesk, but powered by Lua AI technology for intelligent, context-aware customer interactions.

[![npm version](https://badge.fury.io/js/@lua/pop.svg)](https://badge.fury.io/js/@lua/pop)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## ✨ Features

- 🚀 **One-Line Integration** - Add to any website with a single script tag
- 🤖 **AI-Powered Conversations** - Intelligent responses using Lua AI technology
- 🎨 **Highly Customizable** - Colors, positions, themes, and branding
- 📱 **Mobile Responsive** - Perfect experience across all devices
- 🔒 **Secure Authentication** - Token-based security with session management
- 🌐 **Multi-Environment** - Staging and production environments
- 💬 **Rich Media Support** - Images, files, location sharing, and more
- 🎵 **Voice Chat** - Optional voice interaction capabilities
- 🔗 **Deep Integration** - Custom navigation and event handling
- 🌙 **Dark/Light Themes** - Automatic theme switching support
- 📊 **Real-time Updates** - Live message synchronization via WebSockets
- 🎯 **Floating & Embedded** - Multiple display modes for different use cases

## 📦 Installation

### Option 1: CDN Script (Recommended)

Add this to your website's HTML:

```html
<!-- Load the LuaPop widget -->
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  // Initialize with your configuration
  window.LuaPop.init({
    agentId: "your-agent-id",
    sessionId: "unique-user-session", // Optional: for user identification
    position: "bottom-right",
    theme: "light",
    buttonText: "Chat with AI",
    environment: "production" // or "staging"
  });
</script>
```

### Option 2: NPM Package

```bash
npm install @lua/pop
# or
yarn add @lua/pop
# or
pnpm add @lua/pop
```

```tsx
import { LuaPopWidget } from '@lua/pop';
import '@lua/pop/dist/style.css';

function App() {
  return (
    <LuaPopWidget 
      config={{
        agentId: "your-agent-id",
        sessionId: "unique-user-session",
        position: "bottom-right",
        theme: "light",
        buttonText: "Chat with AI"
      }}
      apiUrl="https://api.heylua.ai"
      cdnUrl="https://cdn.heylua.ai"
      authUrl="https://auth.heylua.ai"
    />
  );
}
```

## 🚀 Quick Start

### 1. Basic Floating Widget

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Website</title>
</head>
<body>
  <h1>Welcome to my website!</h1>
  
  <!-- Your existing content -->
  
  <!-- LuaPop Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "your-agent-id",
      position: "bottom-right",
      theme: "light",
      buttonText: "Need Help?",
      chatTitle: "Customer Support"
    });
  </script>
</body>
</html>
```

### 2. Embedded Chat

```html
<div id="chat-container" style="width: 400px; height: 600px;"></div>

<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    displayMode: "embedded",
    embeddedDisplayConfig: {
      targetContainerId: "chat-container"
    },
    theme: "light"
  });
</script>
```

### 3. Custom Styling

```html
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    position: "bottom-right",
    theme: "light",
    buttonColor: "#007bff",
    buttonText: "💬 Chat Now",
    chatTitle: "AI Assistant",
    popupButtonStyles: {
      borderRadius: "25px",
      padding: "15px 20px",
      fontSize: "16px"
    },
    chatTitleHeaderStyles: {
      background: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
      color: "white"
    }
  });
</script>
```

## 🎯 Display Modes

### Floating Widget (Default)
Perfect for most websites - appears as a floating button that opens a chat window.

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  displayMode: "floating", // Default
  position: "bottom-right"
});
```

### Embedded Widget
Integrate directly into your page layout - great for dedicated support pages.

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  displayMode: "embedded",
  embeddedDisplayConfig: {
    targetContainerId: "my-chat-container"
  }
});
```

## 🎨 Customization Options

### Positioning
```javascript
// Available positions
position: "bottom-right" // Default
position: "bottom-left"
position: "top-right"
position: "top-left"
```

### Themes
```javascript
theme: "light" // Clean, professional look
theme: "dark"  // Modern dark theme
```

### Custom Colors
```javascript
buttonColor: "#ff6b6b"     // Custom button color
buttonIcon: "💬"           // Custom button icon/emoji
```

### Custom Styles
```javascript
// Button styling
popupButtonStyles: {
  borderRadius: "50%",
  width: "60px",
  height: "60px",
  fontSize: "24px"
},

// Button container positioning
popupButtonPositionalContainerStyles: {
  bottom: "20px",
  right: "20px"
},

// Chat header styling
chatTitleHeaderStyles: {
  background: "#2c3e50",
  color: "#ecf0f1",
  borderRadius: "10px 10px 0 0"
}
```

### Branding
```javascript
chatTitle: "Customer Support",
chatHeaderSubtitle: {
  visible: true,
  brandName: "Your Company",
  iconUrl: "https://yoursite.com/logo.png",
  linkUrl: "https://yoursite.com"
},
chatInputPlaceholder: "How can we help you today?"
```

## 🔧 Advanced Features

### Voice Chat
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  voiceModeEnabled: true, // Enable voice interactions
  // ... other config
});
```

### Custom Navigation
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  onNavigate: (pathname, options) => {
    // Handle navigation events from the chat
    console.log('Navigate to:', pathname);
    console.log('Query params:', options.query);
    
    // Example: Use with your router
    window.location.href = pathname + '?' + new URLSearchParams(options.query);
  }
});
```

### Event Handling
```javascript
// Listen for widget events
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    const { eventType, data } = event.data;
    
    switch(eventType) {
      case 'widget_opened':
        console.log('Chat opened');
        // Track analytics, show help hints, etc.
        break;
        
      case 'widget_closed':
        console.log('Chat closed');
        break;
        
      case 'message_sent':
        console.log('User sent message:', data);
        break;
        
      case 'message_received':
        console.log('AI responded:', data);
        break;
    }
  }
});

// Resize events for embedded mode
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_RESIZE') {
    const { width, height } = event.data;
    console.log('Widget resized:', width, height);
  }
});
```

### Session Management
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  sessionId: "user-123", // Persistent user identification
  authToken: "your-auth-token", // Optional: for authenticated users
  // ... other config
});
```

## 🌍 Environment Configuration

### Production
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "production", // Uses api.heylua.ai
  // ... other config
});
```

### Staging/Development
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "staging", // Uses api.lua.dev
  // ... other config
});
```

### Custom Environment
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "custom",
  customBaseApiUri: "https://your-custom-api.com",
  // ... other config
});
```

## 📱 Mobile Optimization

LuaPop automatically optimizes for mobile devices:

- **Responsive Design** - Adapts to screen size
- **Touch-Friendly** - Large touch targets
- **Performance** - Lightweight and fast loading
- **Native Feel** - Smooth animations and interactions

### Mobile-Specific Configuration
```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  // Smaller button on mobile
  popupButtonStyles: {
    width: window.innerWidth < 768 ? "50px" : "60px",
    height: window.innerWidth < 768 ? "50px" : "60px"
  },
  // Adjust positioning for mobile
  popupButtonPositionalContainerStyles: {
    bottom: window.innerWidth < 768 ? "15px" : "25px",
    right: window.innerWidth < 768 ? "15px" : "25px"
  }
});
```

## 🔒 Security & Privacy

- **Token-Based Authentication** - Secure API access
- **Session Isolation** - Each user gets a unique session
- **HTTPS Only** - All communications encrypted
- **No Data Storage** - Widget doesn't store personal data locally
- **GDPR Compliant** - Privacy-focused design

## 🎯 Use Cases

### Customer Support
```javascript
window.LuaPop.init({
  agentId: "support-agent",
  chatTitle: "Customer Support",
  buttonText: "Get Help",
  chatInputPlaceholder: "Describe your issue...",
  theme: "light"
});
```

### Sales Assistant
```javascript
window.LuaPop.init({
  agentId: "sales-agent",
  chatTitle: "Sales Assistant",
  buttonText: "💰 Get Quote",
  buttonColor: "#28a745",
  chatInputPlaceholder: "What product interests you?",
  theme: "light"
});
```

### Product Guide
```javascript
window.LuaPop.init({
  agentId: "product-guide",
  chatTitle: "Product Guide",
  buttonText: "🔍 Explore",
  buttonColor: "#6f42c1",
  chatInputPlaceholder: "Ask about our products...",
  voiceModeEnabled: true
});
```

### Embedded Documentation
```javascript
window.LuaPop.init({
  agentId: "docs-assistant",
  displayMode: "embedded",
  embeddedDisplayConfig: {
    targetContainerId: "docs-chat"
  },
  chatTitle: "Documentation Assistant",
  chatInputPlaceholder: "Search documentation..."
});
```

## 🛠️ Development

### Local Development

```bash
# Clone the repository
git clone https://github.com/lua-ai-global/lua-web.git
cd lua-web/packages/lua-pop

# Install dependencies
pnpm install

# Start development server
pnpm dev

# Build for production
pnpm build
```

### Testing Your Integration

1. **Use Staging Environment** for testing
2. **Check Browser Console** for any errors
3. **Test on Multiple Devices** - desktop, tablet, mobile
4. **Verify Events** are firing correctly
5. **Test Different Positions** and themes

### Build Output

The build process generates:
- `lua-pop.umd.js` - Universal module for browser usage
- `style.css` - Stylesheet with all necessary styles
- Source maps for debugging

## 📊 Analytics & Monitoring

Track widget performance and user interactions:

```javascript
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    // Send to your analytics platform
    gtag('event', 'chat_interaction', {
      event_category: 'engagement',
      event_label: event.data.eventType
    });
  }
});
```

## 🔧 Troubleshooting

### Common Issues

**Widget Not Appearing**
- Check console for JavaScript errors
- Verify `agentId` is correct
- Ensure script is loaded after DOM

**Styling Issues**
- Check for CSS conflicts
- Use browser dev tools to inspect styles
- Verify custom styles are valid CSS

**Authentication Errors**
- Verify `agentId` exists and is active
- Check network tab for API errors
- Ensure correct environment is set

### Debug Mode

```javascript
// Enable debug logging
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "staging", // Use staging for debugging
  // ... other config
});

// Check browser console for detailed logs
```

## 📚 API Reference

See [API.md](./API.md) for complete configuration options and methods.

## 🎯 Examples

See [EXAMPLES.md](./EXAMPLES.md) for real-world implementation examples.

## 🔄 Migration Guide

See [MIGRATION.md](./MIGRATION.md) for migrating from other chat widgets.

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## 📄 License

MIT © [Lua AI Global](https://lua.ai)

## 🆘 Support

- **Documentation**: [docs.lua.ai](https://docs.lua.ai)
- **GitHub Issues**: [Report bugs](https://github.com/lua-ai-global/lua-web/issues)
- **Email Support**: [support@heylua.ai](mailto:support@heylua.ai)
- **Discord Community**: [Join our Discord](https://discord.gg/lua-ai)

---

**Ready to get started?** Choose your integration method above and have your AI chat widget running in minutes! 🚀