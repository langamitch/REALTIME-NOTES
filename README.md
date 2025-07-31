# Real-Time Dual-Device Notes with IP-Based Device Identification

This application allows multiple devices to collaborate on a shared note in real-time, with one device acting as the "typer" and others as "viewers". Devices are now identified by their IP addresses instead of random device IDs.

## 🚀 Key Features

- **IP-Based Device Identification**: Devices are identified by their IP addresses for better tracking and management
- **Real-Time Collaboration**: Multiple devices can connect and collaborate on the same note
- **Role Management**: One device acts as the typer while others are viewers
- **Automatic Cleanup**: Devices are automatically removed when they disconnect
- **Heartbeat System**: Keeps devices active and detects disconnections
- **Firebase Integration**: Uses Firebase Authentication and Firestore for real-time data sync

## 🔧 How It Works

### Device Identification

- Each device gets its IP address using the `ipify.org` API
- If the API fails, a fallback IP is generated (192.168.1.x)
- The IP address serves as the unique device identifier

### Connection Process

1. User logs in with email/password
2. Device IP is detected and registered in Firebase
3. If multiple devices are connected, users choose their role (typer/viewer)
4. If only one device is connected, it automatically becomes the typer

### Real-Time Sync

- The typer can edit the note content
- Changes are saved to Firebase after 1 second of inactivity
- All connected devices (typer and viewers) receive real-time updates
- Heartbeat system keeps devices active and detects disconnections

## 📁 Files

- `index.html` - Main application with IP-based device identification
- `test.html` - Test file to verify IP detection works correctly
- `README.md` - This documentation file

## 🛠️ Setup Instructions

1. **Firebase Configuration**: The Firebase config is already included in the code
2. **Open the Application**: Open `index.html` in a web browser
3. **Create Account**: Sign up with an email and password
4. **Test Multiple Devices**: Open the same URL on different devices/browsers
5. **Choose Roles**: When multiple devices connect, choose typer or viewer roles

## 🔍 Testing

1. Open `test.html` to verify IP detection works on your network
2. Open `index.html` on multiple devices/browsers
3. Log in with the same account on all devices
4. Observe how devices are identified by IP and can collaborate

## 🎯 Key Improvements Made

### IP-Based Device Management

- Devices are now identified by IP address instead of random IDs
- Better device tracking and management
- More intuitive device identification in the UI

### Enhanced UI

- Connection status indicators
- Device list showing all connected devices with their IPs
- Clear role indicators (typer/viewer)
- Better status bar with device information

### Improved Reliability

- Heartbeat system to keep devices active
- Automatic cleanup of disconnected devices
- Better error handling and fallbacks
- Page visibility handling for better resource management

### Better User Experience

- Input validation for login
- More descriptive UI text
- Visual connection status indicators
- Device list with role indicators

## 🔧 Technical Details

### Device Registration

```javascript
await deviceRef.set({
  ipAddress: deviceIP,
  lastActive: firebase.firestore.FieldValue.serverTimestamp(),
  role: "pending",
  userAgent: navigator.userAgent,
  timestamp: firebase.firestore.FieldValue.serverTimestamp(),
});
```

### Heartbeat System

- Sends updates every 30 seconds to keep device active
- Automatically stops when page is hidden
- Restarts when page becomes visible again

### Device Cleanup

- Removes device from Firebase on logout
- Handles page unload events
- Cleans up listeners and intervals

## 🚨 Troubleshooting

1. **IP Detection Fails**: The app will use a fallback IP address
2. **Devices Not Connecting**: Check Firebase configuration and network connectivity
3. **Real-Time Updates Not Working**: Verify Firebase rules allow read/write access
4. **Multiple Devices Not Showing**: Ensure all devices are using the same Firebase project

## 📱 Browser Compatibility

- Modern browsers with ES6+ support
- Requires internet connection for Firebase services
- Works on desktop and mobile browsers
