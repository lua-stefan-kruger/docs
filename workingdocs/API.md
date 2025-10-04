# 📖 LuaPop API Reference

Complete API documentation for LuaPop embeddable chat widget.

## 🏗️ Core API

### window.LuaPop.init(config)

Initialize the LuaPop widget with the provided configuration.

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  position: "bottom-right",
  theme: "light"
  // ... other options
});
```

**Returns:** Widget instance with `destroy()` method

## 📋 Configuration Options

### Required Configuration

| Option | Type | Description |
|--------|------|-------------|
| `agentId` | `string` | **Required.** The ID of the AI agent to use for conversations |

### Basic Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `position` | `"bottom-right" \| "bottom-left" \| "top-right" \| "top-left"` | `"bottom-right"` | Widget position on the page |
| `theme` | `"light" \| "dark"` | `"light"` | Visual theme of the widget |
| `buttonText` | `string` | `"Chat with us"` | Text displayed on the chat button |
| `environment` | `"staging" \| "production" \| "custom"` | `"production"` | API environment to use |

### Authentication & Session

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `authToken` | `string` | `""` | Optional authentication token for authenticated users |
| `sessionId` | `string` | Auto-generated | Unique session identifier for the user |
| `customBaseApiUri` | `string` | - | Custom API base URL (when environment is "custom") |

### Display Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `displayMode` | `"floating" \| "embedded"` | `"floating"` | How the widget is displayed |
| `embeddedDisplayConfig` | `EmbeddedConfig` | - | Configuration for embedded mode |
| `chatWindowHeight` | `string \| number` | `"500px"` | Height of the chat window |
| `chatWindowWidth` | `string \| number` | `"350px"` | Width of the chat window |

#### EmbeddedConfig

```typescript
type EmbeddedConfig = {
  targetContainerId: string; // ID of the container element
}
```

### Visual Customization

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `buttonColor` | `string` | `"#007bff"` | Background color of the chat button |
| `buttonIcon` | `string` | `"💬"` | Icon or emoji displayed on the button |
| `chatTitle` | `string` | `"Chat"` | Title displayed in the chat header |

### Advanced Styling

| Option | Type | Description |
|--------|------|-------------|
| `popupButtonStyles` | `React.CSSProperties` | Custom CSS styles for the chat button |
| `popupButtonPositionalContainerStyles` | `React.CSSProperties` | Custom CSS styles for button positioning |
| `chatTitleHeaderStyles` | `React.CSSProperties` | Custom CSS styles for the chat header |

#### Styling Examples

```javascript
// Custom button styling
popupButtonStyles: {
  borderRadius: "50%",
  width: "60px",
  height: "60px",
  fontSize: "24px",
  boxShadow: "0 4px 12px rgba(0,0,0,0.15)"
}

// Custom positioning
popupButtonPositionalContainerStyles: {
  bottom: "20px",
  right: "20px",
  zIndex: "9999"
}

// Custom header styling
chatTitleHeaderStyles: {
  background: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
  color: "white",
  borderRadius: "10px 10px 0 0"
}
```

### Branding & Content

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `chatInputPlaceholder` | `string` | `"Ask anything, about anything"` | Placeholder text for the input field |
| `chatHeaderSubtitle` | `HeaderSubtitle` | - | Subtitle configuration for branding |

#### HeaderSubtitle

```typescript
type HeaderSubtitle = {
  visible: boolean;
  brandName?: string;
  iconUrl?: string;
  linkUrl?: string;
}
```

**Example:**
```javascript
chatHeaderSubtitle: {
  visible: true,
  brandName: "Your Company",
  iconUrl: "https://yoursite.com/logo.png",
  linkUrl: "https://yoursite.com"
}
```

### Advanced Features

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `voiceModeEnabled` | `boolean` | `false` | Enable voice chat functionality |
| `disablePreviewOnLinks` | `boolean` | `false` | Disable automatic link previews |
| `runtimeContext` | `string` | - | Additional context passed to the AI agent |

### Event Handlers

| Option | Type | Description |
|--------|------|-------------|
| `onNavigate` | `(pathname: string, options: NavigateOptions) => void` | Handler for navigation events from the chat |

#### NavigateOptions

```typescript
type NavigateOptions = {
  query: Record<string, string>;
}
```

**Example:**
```javascript
onNavigate: (pathname, options) => {
  console.log('Navigate to:', pathname);
  console.log('Query params:', options.query);
  
  // Handle navigation in your app
  window.location.href = pathname + '?' + new URLSearchParams(options.query);
}
```

## 🎯 Complete Configuration Example

```javascript
window.LuaPop.init({
  // Required
  agentId: "customer-support-agent",
  
  // Basic configuration
  position: "bottom-right",
  theme: "light",
  buttonText: "💬 Need Help?",
  environment: "production",
  
  // Authentication & session
  sessionId: "user-12345",
  authToken: "your-auth-token",
  
  // Display configuration
  displayMode: "floating",
  chatWindowHeight: "600px",
  chatWindowWidth: "400px",
  
  // Visual customization
  buttonColor: "#28a745",
  buttonIcon: "🤖",
  chatTitle: "Customer Support",
  
  // Advanced styling
  popupButtonStyles: {
    borderRadius: "25px",
    padding: "15px 20px",
    fontSize: "16px",
    fontWeight: "600"
  },
  
  popupButtonPositionalContainerStyles: {
    bottom: "30px",
    right: "30px"
  },
  
  chatTitleHeaderStyles: {
    background: "#28a745",
    color: "white",
    fontWeight: "bold"
  },
  
  // Branding & content
  chatInputPlaceholder: "How can we help you today?",
  chatHeaderSubtitle: {
    visible: true,
    brandName: "Your Company",
    iconUrl: "/logo.png",
    linkUrl: "/"
  },
  
  // Advanced features
  voiceModeEnabled: true,
  disablePreviewOnLinks: false,
  runtimeContext: "page:homepage,user:premium",
  
  // Event handlers
  onNavigate: (pathname, options) => {
    // Custom navigation logic
    console.log('Navigate:', pathname, options);
  }
});
```

## 📡 Events API

LuaPop communicates with your website through the `postMessage` API. Listen for these events:

### Widget Events

```javascript
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    const { eventType, data } = event.data;
    
    switch(eventType) {
      case 'widget_opened':
        // Chat widget was opened
        break;
      case 'widget_closed':
        // Chat widget was closed
        break;
      case 'message_sent':
        // User sent a message
        break;
      case 'message_received':
        // AI sent a response
        break;
    }
  }
});
```

#### Event Types

| Event Type | Description | Data |
|------------|-------------|------|
| `widget_opened` | Chat widget opened by user | `{}` |
| `widget_closed` | Chat widget closed by user | `{}` |
| `message_sent` | User sent a message | `{ content: string, timestamp: string }` |
| `message_received` | AI sent a response | `{ content: string, timestamp: string }` |

### Resize Events (Embedded Mode)

```javascript
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_RESIZE') {
    const { width, height } = event.data;
    console.log('Widget resized:', width, height);
  }
});
```

## 🔧 Methods API

### Widget Instance Methods

```javascript
const widget = window.LuaPop.init({ /* config */ });

// Destroy the widget
widget.destroy();
```

#### destroy()

Removes the widget from the page and cleans up all event listeners.

```javascript
const widget = window.LuaPop.init({
  agentId: "support-agent"
});

// Later, remove the widget
widget.destroy();
```

### Global Methods

#### window.LuaPop.config

Access the current widget configuration:

```javascript
console.log(window.LuaPop.config);
// Returns the current configuration object
```

## 🌍 Environment Configuration

### Production Environment

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "production" // Uses api.heylua.ai
});
```

**Endpoints:**
- API: `https://api.heylua.ai`
- CDN: `https://cdn.heylua.ai`
- Auth: `https://auth.heylua.ai`

### Staging Environment

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "staging" // Uses api.lua.dev
});
```

**Endpoints:**
- API: `https://api.lua.dev`
- CDN: `https://cdn.lua.dev`
- Auth: `https://auth.lua.dev`

### Custom Environment

```javascript
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "custom",
  customBaseApiUri: "https://your-api.com"
});
```

## 🎨 CSS Classes & Styling

### Available CSS Classes

LuaPop uses CSS classes with the `lua:` prefix. You can override these for custom styling:

#### Widget Container
```css
.lua-pop-widget {
  /* Main widget container */
}

.lua-pop-floating {
  /* Floating mode container */
}

.lua-pop-embedded {
  /* Embedded mode container */
}
```

#### Button Styling
```css
.lua-pop-button {
  /* Chat button base styles */
}

.lua-pop-button:hover {
  /* Button hover state */
}

.lua-pop-button-container {
  /* Button positioning container */
}
```

#### Chat Window
```css
.lua-pop-chat-window {
  /* Chat window container */
}

.lua-pop-chat-header {
  /* Chat header */
}

.lua-pop-chat-messages {
  /* Messages container */
}

.lua-pop-chat-input {
  /* Input area */
}
```

#### Theme Classes
```css
[data-theme="light"] {
  /* Light theme styles */
}

[data-theme="dark"] {
  /* Dark theme styles */
}
```

### Custom CSS Override Example

```css
/* Override button styles */
.lua-pop-button {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
  border: none !important;
  box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3) !important;
}

/* Override chat header */
.lua-pop-chat-header {
  background: #2c3e50 !important;
  color: white !important;
}

/* Custom animations */
.lua-pop-widget {
  animation: slideInUp 0.3s ease-out;
}

@keyframes slideInUp {
  from {
    transform: translateY(100px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
```

## 🔒 Security & Privacy

### Authentication Flow

1. **Agent Authentication**: Widget authenticates with the specified agent
2. **Session Management**: Unique session ID for each user
3. **Token Validation**: Optional auth tokens for authenticated users
4. **Secure Communication**: All API calls use HTTPS

### Data Handling

- **No Local Storage**: Personal data is not stored locally
- **Session Isolation**: Each user gets a unique session
- **GDPR Compliant**: Privacy-focused design
- **Secure Transmission**: All data encrypted in transit

### Best Practices

```javascript
// Use environment-specific agent IDs
const agentId = process.env.NODE_ENV === 'production' 
  ? 'prod-agent-id' 
  : 'staging-agent-id';

// Generate unique session IDs
const sessionId = `user-${Date.now()}-${Math.random().toString(36).substr(2, 9)}`;

// Implement proper error handling
window.LuaPop.init({
  agentId,
  sessionId,
  environment: process.env.NODE_ENV === 'production' ? 'production' : 'staging'
});
```

## 📊 Analytics Integration

### Google Analytics 4

```javascript
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    gtag('event', 'chat_interaction', {
      event_category: 'engagement',
      event_label: event.data.eventType,
      chat_agent_id: 'your-agent-id'
    });
  }
});
```

### Custom Analytics

```javascript
class ChatAnalytics {
  constructor() {
    this.sessionStart = Date.now();
    this.interactions = [];
  }

  track(eventType, data = {}) {
    const event = {
      type: eventType,
      timestamp: Date.now(),
      sessionDuration: Date.now() - this.sessionStart,
      ...data
    };
    
    this.interactions.push(event);
    
    // Send to your analytics service
    fetch('/api/analytics/chat', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(event)
    });
  }
}

const analytics = new ChatAnalytics();

window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    analytics.track(event.data.eventType, event.data);
  }
});
```

## 🐛 Error Handling

### Common Error Scenarios

#### Agent Not Found
```javascript
// Error: Agent ID doesn't exist
window.LuaPop.init({
  agentId: "non-existent-agent"
});
// Widget will not appear, check browser console
```

#### Network Issues
```javascript
// Handle network failures gracefully
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_ERROR') {
    console.error('LuaPop Error:', event.data.error);
    
    // Show fallback UI or retry logic
    showFallbackSupport();
  }
});
```

#### Container Not Found (Embedded Mode)
```javascript
window.LuaPop.init({
  displayMode: "embedded",
  embeddedDisplayConfig: {
    targetContainerId: "non-existent-container" // Error: container not found
  }
});
```

### Debug Mode

Enable detailed logging for troubleshooting:

```javascript
// Use staging environment for debugging
window.LuaPop.init({
  agentId: "your-agent-id",
  environment: "staging", // More verbose logging
  // ... other config
});

// Check browser console for detailed logs
```

## 📱 Mobile Considerations

### Responsive Configuration

```javascript
function getMobileConfig() {
  const isMobile = window.innerWidth <= 768;
  
  return {
    agentId: "mobile-agent",
    
    // Smaller button on mobile
    popupButtonStyles: {
      width: isMobile ? "50px" : "60px",
      height: isMobile ? "50px" : "60px",
      fontSize: isMobile ? "20px" : "24px"
    },
    
    // Adjusted positioning
    popupButtonPositionalContainerStyles: {
      bottom: isMobile ? "15px" : "25px",
      right: isMobile ? "15px" : "25px"
    },
    
    // Mobile-optimized dimensions
    chatWindowWidth: isMobile ? "100vw" : "350px",
    chatWindowHeight: isMobile ? "100vh" : "500px"
  };
}

window.LuaPop.init(getMobileConfig());
```

### Touch Events

```javascript
// Handle mobile-specific interactions
let touchStartY = 0;

document.addEventListener('touchstart', function(e) {
  touchStartY = e.touches[0].clientY;
});

document.addEventListener('touchend', function(e) {
  const touchEndY = e.changedTouches[0].clientY;
  const swipeDistance = touchStartY - touchEndY;
  
  // Swipe up to open chat
  if (swipeDistance > 100) {
    // Trigger chat open programmatically
    document.querySelector('.lua-pop-button')?.click();
  }
});
```

## 🔧 Advanced Integration Patterns

### Conditional Loading

```javascript
class ConditionalChatLoader {
  constructor() {
    this.shouldLoad = this.checkConditions();
    if (this.shouldLoad) {
      this.loadChat();
    }
  }

  checkConditions() {
    // Only load for certain pages
    if (window.location.pathname === '/support') return true;
    
    // Only load for logged-in users
    if (document.cookie.includes('user_logged_in=true')) return true;
    
    // Only load during business hours
    const hour = new Date().getHours();
    if (hour >= 9 && hour <= 17) return true;
    
    return false;
  }

  loadChat() {
    window.LuaPop.init({
      agentId: "conditional-agent",
      position: "bottom-right",
      theme: "light"
    });
  }
}

new ConditionalChatLoader();
```

### Multi-Agent Setup

```javascript
class MultiAgentChat {
  constructor() {
    this.agents = {
      support: "support-agent-id",
      sales: "sales-agent-id",
      technical: "tech-agent-id"
    };
    
    this.currentAgent = this.determineAgent();
    this.initChat();
  }

  determineAgent() {
    const path = window.location.pathname;
    
    if (path.includes('/pricing') || path.includes('/buy')) {
      return 'sales';
    } else if (path.includes('/docs') || path.includes('/api')) {
      return 'technical';
    } else {
      return 'support';
    }
  }

  initChat() {
    const agentConfigs = {
      support: {
        buttonText: "💬 Support",
        buttonColor: "#007bff",
        chatTitle: "Customer Support"
      },
      sales: {
        buttonText: "💰 Sales",
        buttonColor: "#28a745",
        chatTitle: "Sales Team"
      },
      technical: {
        buttonText: "🔧 Tech Help",
        buttonColor: "#6f42c1",
        chatTitle: "Technical Support"
      }
    };

    const config = agentConfigs[this.currentAgent];

    window.LuaPop.init({
      agentId: this.agents[this.currentAgent],
      ...config,
      position: "bottom-right",
      theme: "light",
      runtimeContext: `agent_type:${this.currentAgent}`
    });
  }
}

new MultiAgentChat();
```

This comprehensive API reference covers all aspects of LuaPop configuration and integration. Use it as your complete guide for implementing and customizing the widget for your specific needs.
