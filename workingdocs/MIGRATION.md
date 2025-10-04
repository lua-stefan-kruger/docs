# 🔄 Migration Guide to LuaPop

This guide helps you migrate from other chat widgets to LuaPop.

## 📦 From Intercom

### Before (Intercom)
```html
<script>
  window.intercomSettings = {
    app_id: "your_app_id",
    name: "John Doe",
    email: "john@example.com",
    created_at: 1312182000
  };
</script>
<script>
  (function(){var w=window;var ic=w.Intercom;if(typeof ic==="function"){ic('reattach_activator');ic('update',w.intercomSettings);}else{var d=document;var i=function(){i.c(arguments);};i.q=[];i.c=function(args){i.q.push(args);};w.Intercom=i;var l=function(){var s=d.createElement('script');s.type='text/javascript';s.async=true;s.src='https://widget.intercom.io/widget/your_app_id';var x=d.getElementsByTagName('script')[0];x.parentNode.insertBefore(s,x);};if(document.readyState==='complete'){l();}else if(w.attachEvent){w.attachEvent('onload',l);}else{w.addEventListener('load',l,false);}}})();
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "your-agent-id",
    sessionId: "john-doe-123", // User identification
    position: "bottom-right",
    theme: "light",
    buttonText: "💬 Message us",
    chatTitle: "Customer Support",
    runtimeContext: "user:john@example.com,created:1312182000"
  });
</script>
```

### Key Migration Points
- ✅ **Simpler Setup** - Single script tag vs complex initialization
- ✅ **AI-Powered** - Intelligent responses vs human-only support
- ✅ **Better Customization** - More styling options
- ✅ **No Monthly Fees** - Pay per usage model

---

## 📦 From Zendesk Chat

### Before (Zendesk Chat)
```html
<script id="ze-snippet" src="https://static.zdassets.com/ekr/snippet.js?key=your-key"></script>
<script>
  zE('webWidget', 'setLocale', 'en-US');
  zE('webWidget', 'updateSettings', {
    webWidget: {
      color: {
        theme: '#78a300'
      },
      position: {
        horizontal: 'right',
        vertical: 'bottom'
      }
    }
  });
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "zendesk-migration-agent",
    position: "bottom-right",
    theme: "light",
    buttonColor: "#78a300",
    chatTitle: "Support",
    buttonText: "💬 Chat",
    environment: "production"
  });
</script>
```

### Migration Benefits
- ✅ **24/7 Availability** - AI never sleeps
- ✅ **Instant Responses** - No waiting for agents
- ✅ **Consistent Quality** - AI provides uniform support
- ✅ **Easy Integration** - Simpler setup process

---

## 📦 From Drift

### Before (Drift)
```html
<script>
"use strict";

!function() {
  var t = window.driftt = window.drift = window.driftt || [];
  if (!t.init) {
    if (t.invoked) return void (window.console && console.error && console.error("Drift snippet included twice."));
    t.invoked = !0, t.methods = [ "identify", "config", "track", "reset", "debug", "show", "ping", "page", "hide", "off", "on" ], 
    t.factory = function(e) {
      return function() {
        var n = Array.prototype.slice.call(arguments);
        return n.unshift(e), t.push(n), t;
      };
    }, t.methods.forEach(function(e) {
      t[e] = t.factory(e);
    }), t.load = function(t) {
      var e = 3e5, n = Math.ceil(new Date() / e) * e, o = document.createElement("script");
      o.type = "text/javascript", o.async = !0, o.crossorigin = "anonymous", o.src = "https://js.driftt.com/include/" + n + "/" + t + ".js";
      var i = document.getElementsByTagName("script")[0];
      i.parentNode.insertBefore(o, i);
    };
  }
}();
drift.SNIPPET_VERSION = '0.3.1';
drift.load('your-drift-id');
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "sales-agent",
    position: "bottom-right",
    theme: "light",
    buttonText: "👋 Let's chat",
    chatTitle: "Sales Team",
    buttonColor: "#2d88ff",
    voiceModeEnabled: true, // Enhanced interaction
    
    // Track events like Drift
    onNavigate: (pathname, options) => {
      console.log('User navigated:', pathname);
    }
  });

  // Listen for chat events (similar to Drift tracking)
  window.addEventListener('message', function(event) {
    if (event.data && event.data.type === 'LUA_POP_EVENT') {
      console.log('Chat event:', event.data.eventType);
      // Send to your analytics
    }
  });
</script>
```

### Drift vs LuaPop
- ✅ **AI-First Approach** - Intelligent conversations from day one
- ✅ **Voice Capabilities** - Optional voice chat feature
- ✅ **Better Mobile Experience** - Optimized for mobile devices
- ✅ **Simpler Implementation** - Less complex setup

---

## 📦 From Crisp

### Before (Crisp)
```html
<script type="text/javascript">
  window.$crisp=[];
  window.CRISP_WEBSITE_ID="your-website-id";
  (function(){
    d=document;
    s=d.createElement("script");
    s.src="https://client.crisp.chat/l.js";
    s.async=1;
    d.getElementsByTagName("head")[0].appendChild(s);
  })();
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "crisp-migration-agent",
    position: "bottom-right",
    theme: "light",
    buttonText: "💬 Chat",
    chatTitle: "Support",
    environment: "production"
  });
</script>
```

---

## 📦 From Tawk.to

### Before (Tawk.to)
```html
<script type="text/javascript">
var Tawk_API=Tawk_API||{}, Tawk_LoadStart=new Date();
(function(){
var s1=document.createElement("script"),s0=document.getElementsByTagName("script")[0];
s1.async=true;
s1.src='https://embed.tawk.to/your-tawk-id/default';
s1.charset='UTF-8';
s1.setAttribute('crossorigin','*');
s0.parentNode.insertBefore(s1,s0);
})();
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "tawk-migration-agent",
    position: "bottom-right",
    theme: "light",
    buttonText: "💬 Chat with us",
    chatTitle: "Live Chat",
    buttonColor: "#00b894"
  });
</script>
```

---

## 📦 From LiveChat

### Before (LiveChat)
```html
<script>
    window.__lc = window.__lc || {};
    window.__lc.license = 12345678;
    ;(function(n,t,c){function i(n){return e._h?e._h.apply(null,n):e._q.push(n)}var e={_q:[],_h:null,_v:"2.0",on:function(){i(["on",c.call(arguments)])},once:function(){i(["once",c.call(arguments)])},off:function(){i(["off",c.call(arguments)])},get:function(){if(!e._h)throw new Error("[LiveChatWidget] You can't use getters before load.");return i(["get",c.call(arguments)])},call:function(){i(["call",c.call(arguments)])},init:function(){var n=t.createElement("script");n.async=!0,n.type="text/javascript",n.src="https://cdn.livechatinc.com/tracking.js",t.head.appendChild(n)}};!n.__lc.asyncInit&&e.init(),n.LiveChatWidget=n.LiveChatWidget||e}(window,document,[].slice))
</script>
```

### After (LuaPop)
```html
<script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
<script>
  window.LuaPop.init({
    agentId: "livechat-migration-agent",
    position: "bottom-right",
    theme: "light",
    buttonText: "💬 Chat now",
    chatTitle: "LiveChat",
    buttonColor: "#ff6900"
  });
</script>
```

---

## 🔄 Configuration Migration Mapping

### Common Configuration Mappings

| Feature | Intercom | Zendesk | Drift | LuaPop |
|---------|----------|---------|-------|---------|
| **App ID** | `app_id` | `key` | `drift-id` | `agentId` |
| **Position** | Not configurable | `position.horizontal/vertical` | Not configurable | `position` |
| **Theme Color** | `color_override` | `color.theme` | `theme.primaryColor` | `buttonColor` |
| **Button Text** | Not configurable | Custom CSS | `teaser.text` | `buttonText` |
| **User ID** | `user_id` | Custom | `userId` | `sessionId` |
| **Custom Data** | `custom_attributes` | Custom fields | `attributes` | `runtimeContext` |

### Event Migration

#### From Intercom Events
```javascript
// Before (Intercom)
Intercom('onShow', function() {
  console.log('Widget opened');
});

Intercom('onHide', function() {
  console.log('Widget closed');
});

// After (LuaPop)
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    switch(event.data.eventType) {
      case 'widget_opened':
        console.log('Widget opened');
        break;
      case 'widget_closed':
        console.log('Widget closed');
        break;
    }
  }
});
```

#### From Zendesk Events
```javascript
// Before (Zendesk)
zE('webWidget:on', 'open', function() {
  console.log('Widget opened');
});

zE('webWidget:on', 'close', function() {
  console.log('Widget closed');
});

// After (LuaPop) - Same as above
```

#### From Drift Events
```javascript
// Before (Drift)
drift.on('ready', function(api) {
  api.widget.show();
});

drift.on('message', function(e) {
  console.log('Message sent:', e);
});

// After (LuaPop)
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    if (event.data.eventType === 'message_sent') {
      console.log('Message sent:', event.data);
    }
  }
});
```

---

## 🎨 Styling Migration

### From Custom CSS to LuaPop Styling

#### Intercom Custom CSS
```css
/* Before - Intercom custom CSS */
.intercom-launcher {
  background: #ff6b6b !important;
  border-radius: 50% !important;
}

.intercom-messenger-frame {
  border-radius: 10px !important;
}
```

#### LuaPop Equivalent
```javascript
// After - LuaPop configuration
window.LuaPop.init({
  agentId: "your-agent-id",
  buttonColor: "#ff6b6b",
  
  popupButtonStyles: {
    borderRadius: "50%"
  },
  
  chatTitleHeaderStyles: {
    borderRadius: "10px 10px 0 0"
  }
});
```

### Responsive Design Migration

```javascript
// Responsive configuration for all screen sizes
function getResponsiveConfig() {
  const isMobile = window.innerWidth <= 768;
  const isTablet = window.innerWidth <= 1024 && window.innerWidth > 768;
  
  return {
    agentId: "responsive-agent",
    
    // Responsive button sizing
    popupButtonStyles: {
      width: isMobile ? "50px" : isTablet ? "55px" : "60px",
      height: isMobile ? "50px" : isTablet ? "55px" : "60px",
      fontSize: isMobile ? "20px" : isTablet ? "22px" : "24px"
    },
    
    // Responsive positioning
    popupButtonPositionalContainerStyles: {
      bottom: isMobile ? "15px" : "25px",
      right: isMobile ? "15px" : "25px"
    },
    
    // Responsive chat window
    chatWindowWidth: isMobile ? "100vw" : isTablet ? "380px" : "400px",
    chatWindowHeight: isMobile ? "100vh" : "600px"
  };
}

window.LuaPop.init(getResponsiveConfig());
```

---

## 📊 Analytics Migration

### Google Analytics Integration

#### From Intercom Analytics
```javascript
// Before (Intercom + GA)
Intercom('onShow', function() {
  gtag('event', 'intercom_opened', {
    event_category: 'engagement'
  });
});
```

#### To LuaPop Analytics
```javascript
// After (LuaPop + GA)
window.addEventListener('message', function(event) {
  if (event.data && event.data.type === 'LUA_POP_EVENT') {
    gtag('event', 'luapop_' + event.data.eventType, {
      event_category: 'engagement',
      event_label: 'ai_chat'
    });
  }
});
```

### Custom Analytics Migration

```javascript
// Universal analytics wrapper for any previous solution
class ChatAnalyticsMigration {
  constructor() {
    this.previousProvider = 'intercom'; // or 'zendesk', 'drift', etc.
    this.setupLuaPopTracking();
  }

  setupLuaPopTracking() {
    window.addEventListener('message', (event) => {
      if (event.data && event.data.type === 'LUA_POP_EVENT') {
        this.trackEvent(event.data.eventType, event.data);
      }
    });
  }

  trackEvent(eventType, data) {
    // Send to your analytics service
    const event = {
      provider: 'luapop',
      previous_provider: this.previousProvider,
      event_type: eventType,
      timestamp: Date.now(),
      data: data
    };

    // Send to your analytics endpoint
    fetch('/api/analytics', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(event)
    });

    // Also send to Google Analytics
    if (typeof gtag !== 'undefined') {
      gtag('event', 'chat_' + eventType, {
        event_category: 'luapop_migration',
        event_label: this.previousProvider
      });
    }
  }
}

new ChatAnalyticsMigration();
```

---

## 🔧 Advanced Migration Scenarios

### Multi-Environment Migration

```javascript
// Migrate different environments gradually
class GradualMigration {
  constructor() {
    this.migrationPercentage = 25; // Start with 25% of users
    this.shouldUseLuaPop = this.determineMigration();
    
    if (this.shouldUseLuaPop) {
      this.initLuaPop();
    } else {
      this.initLegacyChat();
    }
  }

  determineMigration() {
    // Check if user is in migration group
    const userId = this.getUserId();
    const hash = this.simpleHash(userId);
    return (hash % 100) < this.migrationPercentage;
  }

  simpleHash(str) {
    let hash = 0;
    for (let i = 0; i < str.length; i++) {
      const char = str.charCodeAt(i);
      hash = ((hash << 5) - hash) + char;
      hash = hash & hash; // Convert to 32-bit integer
    }
    return Math.abs(hash);
  }

  getUserId() {
    // Get user ID from your system
    return localStorage.getItem('user_id') || 'anonymous';
  }

  initLuaPop() {
    console.log('Loading LuaPop for user');
    window.LuaPop.init({
      agentId: "migration-agent",
      position: "bottom-right",
      theme: "light",
      runtimeContext: "migration:true"
    });
  }

  initLegacyChat() {
    console.log('Loading legacy chat for user');
    // Initialize your previous chat solution
    // This allows for gradual rollout and easy rollback
  }
}

new GradualMigration();
```

### A/B Testing Migration

```javascript
// Test LuaPop against existing solution
class MigrationABTest {
  constructor() {
    this.variant = this.getVariant();
    this.initChat();
    this.trackVariant();
  }

  getVariant() {
    const stored = localStorage.getItem('chat_migration_variant');
    if (stored) return stored;

    const variant = Math.random() < 0.5 ? 'luapop' : 'legacy';
    localStorage.setItem('chat_migration_variant', variant);
    return variant;
  }

  initChat() {
    if (this.variant === 'luapop') {
      window.LuaPop.init({
        agentId: "ab-test-agent",
        position: "bottom-right",
        theme: "light",
        runtimeContext: "ab_test:luapop"
      });
    } else {
      // Initialize legacy chat
      this.initLegacyChat();
    }
  }

  trackVariant() {
    gtag('event', 'chat_ab_test', {
      event_category: 'experiment',
      event_label: this.variant
    });
  }

  initLegacyChat() {
    // Your existing chat initialization
    console.log('Loading legacy chat for A/B test');
  }
}

new MigrationABTest();
```

---

## 📋 Migration Checklist

### Pre-Migration
- [ ] **Audit Current Setup** - Document existing configuration
- [ ] **Identify Custom Features** - Note any custom integrations
- [ ] **Plan Agent Configuration** - Set up LuaPop agents
- [ ] **Test in Staging** - Verify LuaPop works in your environment

### During Migration
- [ ] **Gradual Rollout** - Start with small percentage of users
- [ ] **Monitor Performance** - Track engagement metrics
- [ ] **Collect Feedback** - Gather user feedback on new experience
- [ ] **Compare Analytics** - Ensure tracking is working correctly

### Post-Migration
- [ ] **Remove Legacy Code** - Clean up old chat widget code
- [ ] **Update Documentation** - Document new implementation
- [ ] **Train Team** - Ensure team knows how to use new system
- [ ] **Optimize Configuration** - Fine-tune based on usage data

---

## 🆘 Migration Support

### Common Migration Issues

**Multiple Chat Widgets Appearing**
```javascript
// Ensure old widget is removed before initializing LuaPop
if (window.Intercom) {
  window.Intercom('shutdown');
}
if (window.drift) {
  window.drift.reset();
}

// Then initialize LuaPop
window.LuaPop.init({ /* config */ });
```

**Styling Conflicts**
```css
/* Hide legacy chat elements */
.intercom-launcher,
.drift-frame-controller,
.crisp-client {
  display: none !important;
}
```

**Analytics Double-Tracking**
```javascript
// Prevent double tracking during migration
const isMigrated = localStorage.getItem('chat_migrated') === 'true';

if (!isMigrated) {
  // Track migration event
  gtag('event', 'chat_migration_complete', {
    event_category: 'migration',
    previous_provider: 'intercom' // or your previous provider
  });
  
  localStorage.setItem('chat_migrated', 'true');
}
```

### Need Help?

- **Migration Support**: [migration@heylua.ai](mailto:migration@heylua.ai)
- **Technical Questions**: [support@heylua.ai](mailto:support@heylua.ai)
- **Documentation**: [docs.lua.ai](https://docs.lua.ai)
- **Community**: [Discord](https://discord.gg/lua-ai)

---

**Ready to migrate?** Start with our [Quick Start Guide](./QUICKSTART.md) and you'll be up and running in minutes! 🚀
