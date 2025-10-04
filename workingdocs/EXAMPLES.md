# 📚 LuaPop Examples

Real-world implementation examples for different use cases and platforms.

## 🎯 Basic Examples

### 1. Simple Customer Support Widget

Perfect for any website that needs basic customer support.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Business Website</title>
</head>
<body>
  <header>
    <h1>Welcome to Our Business</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#services">Services</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <main>
    <section id="hero">
      <h2>We're here to help!</h2>
      <p>Get instant support with our AI assistant.</p>
    </section>
  </main>

  <!-- LuaPop Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "customer-support",
      chatTitle: "Customer Support",
      buttonText: "💬 Get Help",
      position: "bottom-right",
      theme: "light",
      chatInputPlaceholder: "How can we help you today?",
      environment: "production"
    });
  </script>
</body>
</html>
```

### 2. E-commerce Sales Assistant

Boost sales with an AI shopping assistant.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Online Store</title>
  <style>
    .product-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
    .product-card { border: 1px solid #ddd; padding: 20px; border-radius: 8px; }
  </style>
</head>
<body>
  <header>
    <h1>🛍️ Amazing Store</h1>
    <div class="cart">Cart (0)</div>
  </header>

  <main>
    <div class="product-grid">
      <div class="product-card">
        <h3>Product 1</h3>
        <p>$29.99</p>
        <button>Add to Cart</button>
      </div>
      <div class="product-card">
        <h3>Product 2</h3>
        <p>$39.99</p>
        <button>Add to Cart</button>
      </div>
    </div>
  </main>

  <!-- Shopping Assistant Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "shopping-assistant",
      chatTitle: "Shopping Assistant",
      buttonText: "🛒 Shop Help",
      buttonColor: "#e74c3c",
      position: "bottom-right",
      theme: "light",
      chatInputPlaceholder: "What are you looking for?",
      chatHeaderSubtitle: {
        visible: true,
        brandName: "Amazing Store",
        iconUrl: "/favicon.ico",
        linkUrl: "/"
      },
      // Track shopping events
      onNavigate: (pathname, options) => {
        // Navigate to product pages
        if (pathname.startsWith('/product/')) {
          window.location.href = pathname;
        }
      }
    });

    // Track cart events
    window.addEventListener('message', function(event) {
      if (event.data && event.data.type === 'LUA_POP_EVENT') {
        if (event.data.eventType === 'widget_opened') {
          // Track shopping assistant usage
          console.log('Shopping assistant opened');
        }
      }
    });
  </script>
</body>
</html>
```

### 3. SaaS Product Onboarding

Help users get started with your software.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SaaS Dashboard</title>
  <style>
    .dashboard { display: grid; grid-template-columns: 250px 1fr; height: 100vh; }
    .sidebar { background: #2c3e50; color: white; padding: 20px; }
    .main-content { padding: 20px; }
    .welcome-banner { background: #3498db; color: white; padding: 15px; border-radius: 5px; margin-bottom: 20px; }
  </style>
</head>
<body>
  <div class="dashboard">
    <aside class="sidebar">
      <h2>My SaaS App</h2>
      <nav>
        <ul>
          <li><a href="#dashboard">Dashboard</a></li>
          <li><a href="#analytics">Analytics</a></li>
          <li><a href="#settings">Settings</a></li>
        </ul>
      </nav>
    </aside>

    <main class="main-content">
      <div class="welcome-banner">
        <h3>Welcome! 👋</h3>
        <p>Need help getting started? Our AI assistant is here to guide you!</p>
      </div>

      <div class="content">
        <h2>Dashboard</h2>
        <p>Your app content goes here...</p>
      </div>
    </main>
  </div>

  <!-- Onboarding Assistant -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    // Check if user is new
    const isNewUser = !localStorage.getItem('user_onboarded');
    
    window.LuaPop.init({
      agentId: "onboarding-assistant",
      chatTitle: "Onboarding Assistant",
      buttonText: isNewUser ? "🚀 Get Started" : "💡 Need Help?",
      buttonColor: "#9b59b6",
      position: "bottom-right",
      theme: "light",
      chatInputPlaceholder: "Ask me anything about the app...",
      voiceModeEnabled: true,
      
      // Custom session for user context
      sessionId: `user-${Date.now()}`,
      
      // Handle navigation within the app
      onNavigate: (pathname, options) => {
        // Navigate to different sections
        const section = pathname.replace('/', '');
        const element = document.getElementById(section);
        if (element) {
          element.scrollIntoView({ behavior: 'smooth' });
        }
      }
    });

    // Auto-open for new users
    if (isNewUser) {
      setTimeout(() => {
        // Simulate button click to open chat
        document.querySelector('[data-testid="chat-button"]')?.click();
        localStorage.setItem('user_onboarded', 'true');
      }, 2000);
    }
  </script>
</body>
</html>
```

## 🏢 Industry-Specific Examples

### 4. Hotel Booking Assistant

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Luxury Hotel</title>
  <style>
    .hero { background: url('/hotel-bg.jpg') center/cover; height: 60vh; display: flex; align-items: center; justify-content: center; color: white; }
    .booking-form { background: rgba(255,255,255,0.9); padding: 30px; border-radius: 10px; }
  </style>
</head>
<body>
  <header>
    <h1>🏨 Luxury Resort & Spa</h1>
  </header>

  <section class="hero">
    <div class="booking-form">
      <h2>Book Your Stay</h2>
      <form>
        <input type="date" placeholder="Check-in">
        <input type="date" placeholder="Check-out">
        <select>
          <option>1 Guest</option>
          <option>2 Guests</option>
          <option>3+ Guests</option>
        </select>
        <button type="submit">Search Rooms</button>
      </form>
    </div>
  </section>

  <!-- Hotel Concierge Assistant -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "hotel-concierge",
      chatTitle: "Hotel Concierge",
      buttonText: "🛎️ Concierge",
      buttonColor: "#d4af37", // Gold color
      position: "bottom-right",
      theme: "light",
      chatInputPlaceholder: "How can I assist with your stay?",
      
      // Elegant styling
      popupButtonStyles: {
        borderRadius: "50%",
        width: "70px",
        height: "70px",
        fontSize: "24px",
        boxShadow: "0 4px 20px rgba(212, 175, 55, 0.3)"
      },
      
      chatTitleHeaderStyles: {
        background: "linear-gradient(135deg, #d4af37, #ffd700)",
        color: "#2c3e50"
      },
      
      chatHeaderSubtitle: {
        visible: true,
        brandName: "Luxury Resort & Spa",
        iconUrl: "/hotel-logo.png",
        linkUrl: "/"
      }
    });
  </script>
</body>
</html>
```

### 5. Healthcare Patient Portal

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Patient Portal</title>
  <style>
    .patient-portal { max-width: 1200px; margin: 0 auto; padding: 20px; }
    .quick-actions { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin: 20px 0; }
    .action-card { background: #f8f9fa; padding: 20px; border-radius: 8px; text-align: center; }
  </style>
</head>
<body>
  <div class="patient-portal">
    <header>
      <h1>🏥 HealthCare Portal</h1>
      <p>Welcome back, John Doe</p>
    </header>

    <div class="quick-actions">
      <div class="action-card">
        <h3>📅 Appointments</h3>
        <p>Schedule or view appointments</p>
      </div>
      <div class="action-card">
        <h3>💊 Prescriptions</h3>
        <p>Refill prescriptions</p>
      </div>
      <div class="action-card">
        <h3>📋 Test Results</h3>
        <p>View lab results</p>
      </div>
      <div class="action-card">
        <h3>💬 Messages</h3>
        <p>Contact your doctor</p>
      </div>
    </div>
  </div>

  <!-- Healthcare Assistant -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "healthcare-assistant",
      chatTitle: "Healthcare Assistant",
      buttonText: "🩺 Ask Assistant",
      buttonColor: "#2ecc71",
      position: "bottom-right",
      theme: "light",
      chatInputPlaceholder: "How can I help with your healthcare needs?",
      
      // Healthcare-specific session
      sessionId: "patient-john-doe-123",
      
      // HIPAA-compliant styling
      chatTitleHeaderStyles: {
        background: "#2ecc71",
        color: "white"
      },
      
      // Disable link previews for privacy
      disablePreviewOnLinks: true
    });

    // Healthcare-specific event tracking
    window.addEventListener('message', function(event) {
      if (event.data && event.data.type === 'LUA_POP_EVENT') {
        // Log healthcare interactions (ensure HIPAA compliance)
        console.log('Healthcare assistant interaction:', event.data.eventType);
      }
    });
  </script>
</body>
</html>
```

## 🔧 Advanced Integration Examples

### 6. Multi-Language Support

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Global Company</title>
</head>
<body>
  <header>
    <h1>Global Business</h1>
    <div class="language-selector">
      <select id="language-select">
        <option value="en">English</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
        <option value="de">Deutsch</option>
      </select>
    </div>
  </header>

  <main>
    <h2>Welcome to our global platform</h2>
  </main>

  <!-- Multi-language Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    const translations = {
      en: {
        chatTitle: "Customer Support",
        buttonText: "💬 Chat",
        placeholder: "How can we help you?"
      },
      es: {
        chatTitle: "Soporte al Cliente",
        buttonText: "💬 Chat",
        placeholder: "¿Cómo podemos ayudarte?"
      },
      fr: {
        chatTitle: "Support Client",
        buttonText: "💬 Chat",
        placeholder: "Comment pouvons-nous vous aider?"
      },
      de: {
        chatTitle: "Kundensupport",
        buttonText: "💬 Chat",
        placeholder: "Wie können wir Ihnen helfen?"
      }
    };

    let currentLanguage = localStorage.getItem('language') || 'en';
    
    function initializeChat(language) {
      const config = translations[language];
      
      window.LuaPop.init({
        agentId: `support-${language}`, // Different agents per language
        chatTitle: config.chatTitle,
        buttonText: config.buttonText,
        chatInputPlaceholder: config.placeholder,
        position: "bottom-right",
        theme: "light",
        sessionId: `user-${language}-${Date.now()}`,
        runtimeContext: `language:${language}` // Pass language context
      });
    }

    // Initialize with current language
    initializeChat(currentLanguage);

    // Handle language changes
    document.getElementById('language-select').addEventListener('change', function(e) {
      currentLanguage = e.target.value;
      localStorage.setItem('language', currentLanguage);
      
      // Reinitialize widget with new language
      initializeChat(currentLanguage);
    });

    // Set initial language selector value
    document.getElementById('language-select').value = currentLanguage;
  </script>
</body>
</html>
```

### 7. Conditional Loading Based on User Behavior

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Smart Loading Example</title>
</head>
<body>
  <header>
    <h1>Smart Website</h1>
  </header>

  <main>
    <section id="pricing">
      <h2>Our Pricing</h2>
      <div class="pricing-cards">
        <div class="card">Basic - $9/month</div>
        <div class="card">Pro - $29/month</div>
        <div class="card">Enterprise - Contact us</div>
      </div>
    </section>

    <section id="features">
      <h2>Features</h2>
      <p>Discover our amazing features...</p>
    </section>
  </main>

  <!-- Smart Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    class SmartChatLoader {
      constructor() {
        this.userBehavior = {
          timeOnSite: 0,
          pagesViewed: 1,
          scrollDepth: 0,
          viewedPricing: false,
          exitIntent: false
        };
        
        this.chatLoaded = false;
        this.init();
      }

      init() {
        this.trackTimeOnSite();
        this.trackScrollDepth();
        this.trackPricingView();
        this.trackExitIntent();
      }

      trackTimeOnSite() {
        setInterval(() => {
          this.userBehavior.timeOnSite += 1;
          this.checkShouldLoadChat();
        }, 1000);
      }

      trackScrollDepth() {
        window.addEventListener('scroll', () => {
          const scrollPercent = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
          this.userBehavior.scrollDepth = Math.max(this.userBehavior.scrollDepth, scrollPercent);
          this.checkShouldLoadChat();
        });
      }

      trackPricingView() {
        const pricingSection = document.getElementById('pricing');
        const observer = new IntersectionObserver((entries) => {
          if (entries[0].isIntersecting) {
            this.userBehavior.viewedPricing = true;
            this.checkShouldLoadChat();
          }
        });
        observer.observe(pricingSection);
      }

      trackExitIntent() {
        document.addEventListener('mouseleave', (e) => {
          if (e.clientY <= 0) {
            this.userBehavior.exitIntent = true;
            this.loadChat('exit-intent');
          }
        });
      }

      checkShouldLoadChat() {
        if (this.chatLoaded) return;

        // Load chat if user has been on site for 30+ seconds
        if (this.userBehavior.timeOnSite >= 30) {
          this.loadChat('time-based');
          return;
        }

        // Load chat if user scrolled 50%+ and viewed pricing
        if (this.userBehavior.scrollDepth >= 50 && this.userBehavior.viewedPricing) {
          this.loadChat('engagement-based');
          return;
        }
      }

      loadChat(trigger) {
        if (this.chatLoaded) return;
        
        this.chatLoaded = true;
        console.log(`Loading chat due to: ${trigger}`);

        // Different configurations based on trigger
        const configs = {
          'time-based': {
            agentId: "general-support",
            buttonText: "💬 Questions?",
            chatTitle: "How can we help?"
          },
          'engagement-based': {
            agentId: "sales-assistant",
            buttonText: "💰 Get Quote",
            chatTitle: "Sales Assistant",
            buttonColor: "#e74c3c"
          },
          'exit-intent': {
            agentId: "retention-specialist",
            buttonText: "⚡ Wait!",
            chatTitle: "Before you go...",
            buttonColor: "#f39c12"
          }
        };

        const config = configs[trigger];

        window.LuaPop.init({
          ...config,
          position: "bottom-right",
          theme: "light",
          sessionId: `user-${trigger}-${Date.now()}`,
          runtimeContext: `trigger:${trigger}`,
          
          // Auto-open for exit intent
          ...(trigger === 'exit-intent' && {
            // Custom logic to auto-open would go here
          })
        });

        // Track the trigger
        if (typeof gtag !== 'undefined') {
          gtag('event', 'chat_loaded', {
            event_category: 'engagement',
            event_label: trigger
          });
        }
      }
    }

    // Initialize smart loading
    new SmartChatLoader();
  </script>
</body>
</html>
```

### 8. A/B Testing Different Configurations

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>A/B Testing Example</title>
</head>
<body>
  <header>
    <h1>A/B Test Website</h1>
  </header>

  <main>
    <h2>Welcome to our site!</h2>
    <p>We're testing different chat configurations to improve user experience.</p>
  </main>

  <!-- A/B Testing Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    class ChatABTest {
      constructor() {
        this.variants = {
          control: {
            agentId: "standard-support",
            buttonText: "Support",
            buttonColor: "#007bff",
            position: "bottom-right",
            theme: "light"
          },
          variant_a: {
            agentId: "friendly-support",
            buttonText: "👋 Need Help?",
            buttonColor: "#28a745",
            position: "bottom-right",
            theme: "light",
            voiceModeEnabled: true
          },
          variant_b: {
            agentId: "proactive-support",
            buttonText: "💬 Chat Now",
            buttonColor: "#dc3545",
            position: "bottom-left",
            theme: "dark"
          }
        };
        
        this.init();
      }

      init() {
        const variant = this.getVariant();
        const config = this.variants[variant];
        
        // Track variant assignment
        this.trackVariant(variant);
        
        // Initialize chat with variant config
        window.LuaPop.init({
          ...config,
          sessionId: `ab-test-${variant}-${Date.now()}`,
          runtimeContext: `ab_variant:${variant}`,
          chatInputPlaceholder: "How can we help you today?"
        });

        // Track interactions
        this.trackInteractions(variant);
      }

      getVariant() {
        // Check if user already has a variant assigned
        let variant = localStorage.getItem('chat_ab_variant');
        
        if (!variant) {
          // Assign random variant (33.33% each)
          const random = Math.random();
          if (random < 0.33) {
            variant = 'control';
          } else if (random < 0.66) {
            variant = 'variant_a';
          } else {
            variant = 'variant_b';
          }
          
          localStorage.setItem('chat_ab_variant', variant);
        }
        
        return variant;
      }

      trackVariant(variant) {
        // Track variant assignment
        if (typeof gtag !== 'undefined') {
          gtag('event', 'ab_test_assigned', {
            event_category: 'experiment',
            event_label: variant,
            custom_parameter_1: variant
          });
        }

        console.log(`A/B Test - Assigned variant: ${variant}`);
      }

      trackInteractions(variant) {
        window.addEventListener('message', function(event) {
          if (event.data && event.data.type === 'LUA_POP_EVENT') {
            // Track all chat interactions with variant info
            if (typeof gtag !== 'undefined') {
              gtag('event', `chat_${event.data.eventType}`, {
                event_category: 'ab_test_interaction',
                event_label: variant,
                ab_variant: variant
              });
            }

            console.log(`A/B Test - ${variant} - ${event.data.eventType}`);
          }
        });
      }
    }

    // Initialize A/B test
    new ChatABTest();
  </script>
</body>
</html>
```

## 📱 Mobile-Specific Examples

### 9. Progressive Web App Integration

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PWA with Chat</title>
  <link rel="manifest" href="/manifest.json">
  <style>
    .pwa-app { max-width: 400px; margin: 0 auto; padding: 20px; }
    .mobile-optimized { font-size: 16px; line-height: 1.5; }
  </style>
</head>
<body>
  <div class="pwa-app">
    <header>
      <h1>📱 My PWA</h1>
      <button id="install-btn" style="display: none;">Install App</button>
    </header>

    <main class="mobile-optimized">
      <h2>Welcome to our PWA!</h2>
      <p>This app works offline and can be installed on your device.</p>
    </main>
  </div>

  <!-- PWA-Optimized Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    // PWA installation logic
    let deferredPrompt;
    
    window.addEventListener('beforeinstallprompt', (e) => {
      e.preventDefault();
      deferredPrompt = e;
      document.getElementById('install-btn').style.display = 'block';
    });

    document.getElementById('install-btn').addEventListener('click', async () => {
      if (deferredPrompt) {
        deferredPrompt.prompt();
        const { outcome } = await deferredPrompt.userChoice;
        console.log(`User response to the install prompt: ${outcome}`);
        deferredPrompt = null;
      }
    });

    // Mobile-optimized chat configuration
    function initMobileChat() {
      const isMobile = window.innerWidth <= 768;
      const isStandalone = window.matchMedia('(display-mode: standalone)').matches;
      
      window.LuaPop.init({
        agentId: "mobile-assistant",
        chatTitle: "Mobile Assistant",
        buttonText: isMobile ? "💬" : "💬 Chat",
        position: "bottom-right",
        theme: "light",
        
        // Mobile-specific styling
        popupButtonStyles: {
          width: isMobile ? "50px" : "60px",
          height: isMobile ? "50px" : "60px",
          fontSize: isMobile ? "20px" : "24px"
        },
        
        popupButtonPositionalContainerStyles: {
          bottom: isMobile ? "15px" : "25px",
          right: isMobile ? "15px" : "25px",
          zIndex: "9999"
        },
        
        // PWA context
        runtimeContext: `pwa:${isStandalone ? 'installed' : 'browser'}`,
        sessionId: `pwa-user-${Date.now()}`
      });
    }

    // Initialize chat
    initMobileChat();

    // Reinitialize on orientation change
    window.addEventListener('orientationchange', () => {
      setTimeout(initMobileChat, 100);
    });
  </script>
</body>
</html>
```

### 10. React Native WebView Integration

```jsx
// React Native component
import React, { useRef, useEffect } from 'react';
import { WebView } from 'react-native-webview';
import { View, StyleSheet } from 'react-native';

const ChatWebView = () => {
  const webViewRef = useRef(null);

  const htmlContent = `
    <!DOCTYPE html>
    <html>
    <head>
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <style>
        body { 
          margin: 0; 
          padding: 0; 
          font-family: -apple-system, BlinkMacSystemFont, sans-serif;
        }
        .container { 
          height: 100vh; 
          display: flex; 
          flex-direction: column; 
        }
        .header { 
          background: #007AFF; 
          color: white; 
          padding: 15px; 
          text-align: center; 
        }
        .chat-area { 
          flex: 1; 
          position: relative; 
        }
      </style>
    </head>
    <body>
      <div class="container">
        <div class="header">
          <h3>Customer Support</h3>
        </div>
        <div class="chat-area" id="chat-container"></div>
      </div>

      <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
      <script>
        // Initialize embedded chat for React Native
        window.LuaPop.init({
          agentId: "mobile-app-support",
          displayMode: "embedded",
          embeddedDisplayConfig: {
            targetContainerId: "chat-container"
          },
          theme: "light",
          chatInputPlaceholder: "Type your message...",
          sessionId: "rn-user-${Date.now()}",
          runtimeContext: "platform:react-native"
        });

        // Send messages to React Native
        window.addEventListener('message', function(event) {
          if (event.data && event.data.type === 'LUA_POP_EVENT') {
            // Send to React Native
            window.ReactNativeWebView?.postMessage(JSON.stringify({
              type: 'CHAT_EVENT',
              data: event.data
            }));
          }
        });
      </script>
    </body>
    </html>
  `;

  const handleMessage = (event) => {
    try {
      const message = JSON.parse(event.nativeEvent.data);
      if (message.type === 'CHAT_EVENT') {
        console.log('Chat event from WebView:', message.data);
        // Handle chat events in React Native
      }
    } catch (error) {
      console.error('Error parsing WebView message:', error);
    }
  };

  return (
    <View style={styles.container}>
      <WebView
        ref={webViewRef}
        source={{ html: htmlContent }}
        style={styles.webView}
        onMessage={handleMessage}
        javaScriptEnabled={true}
        domStorageEnabled={true}
        startInLoadingState={true}
        scalesPageToFit={true}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  webView: {
    flex: 1,
  },
});

export default ChatWebView;
```

## 🎨 Custom Styling Examples

### 11. Glassmorphism Theme

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Glassmorphism Chat</title>
  <style>
    body {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      margin: 0;
      font-family: 'Inter', sans-serif;
    }
    .content {
      padding: 50px;
      color: white;
    }
  </style>
</head>
<body>
  <div class="content">
    <h1>Glassmorphism Design</h1>
    <p>Beautiful glass-like chat widget</p>
  </div>

  <!-- Glassmorphism Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "design-assistant",
      chatTitle: "Design Assistant",
      buttonText: "✨",
      position: "bottom-right",
      theme: "light",
      
      // Glassmorphism button styling
      popupButtonStyles: {
        background: "rgba(255, 255, 255, 0.25)",
        backdropFilter: "blur(10px)",
        border: "1px solid rgba(255, 255, 255, 0.18)",
        borderRadius: "50%",
        width: "60px",
        height: "60px",
        fontSize: "24px",
        color: "white",
        boxShadow: "0 8px 32px 0 rgba(31, 38, 135, 0.37)"
      },
      
      // Glassmorphism chat header
      chatTitleHeaderStyles: {
        background: "rgba(255, 255, 255, 0.25)",
        backdropFilter: "blur(10px)",
        border: "1px solid rgba(255, 255, 255, 0.18)",
        color: "white",
        borderRadius: "15px 15px 0 0"
      }
    });
  </script>
</body>
</html>
```

### 12. Neumorphism Theme

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Neumorphism Chat</title>
  <style>
    body {
      background: #e0e5ec;
      min-height: 100vh;
      margin: 0;
      font-family: 'Inter', sans-serif;
    }
    .content {
      padding: 50px;
      color: #333;
    }
  </style>
</head>
<body>
  <div class="content">
    <h1>Neumorphism Design</h1>
    <p>Soft, extruded chat widget</p>
  </div>

  <!-- Neumorphism Chat Widget -->
  <script src="https://lua-ai-global.github.io/lua-pop/lua-pop.umd.js"></script>
  <script>
    window.LuaPop.init({
      agentId: "neuro-assistant",
      chatTitle: "Assistant",
      buttonText: "💬",
      position: "bottom-right",
      theme: "light",
      
      // Neumorphism button styling
      popupButtonStyles: {
        background: "#e0e5ec",
        borderRadius: "50%",
        width: "60px",
        height: "60px",
        fontSize: "24px",
        color: "#333",
        border: "none",
        boxShadow: "9px 9px 16px #a3b1c6, -9px -9px 16px #ffffff"
      },
      
      // Neumorphism chat header
      chatTitleHeaderStyles: {
        background: "#e0e5ec",
        color: "#333",
        borderRadius: "15px 15px 0 0",
        boxShadow: "inset 5px 5px 10px #a3b1c6, inset -5px -5px 10px #ffffff"
      }
    });
  </script>
</body>
</html>
```

These examples demonstrate the flexibility and power of LuaPop across different industries, platforms, and design approaches. Each example is production-ready and can be customized further based on your specific needs.
