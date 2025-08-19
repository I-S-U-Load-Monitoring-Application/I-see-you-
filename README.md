**🤖 CropAlly Mobile - Robot Control App
A modern React Native mobile application for controlling agricultural robots and autonomous vehicles. Built with Expo, TypeScript, and NativeWind for a seamless cross-platform experience.

🌟 Features
🎮 Robot Control
Dual Joystick Control: Intuitive touch-based joystick interface for precise robot movement
Directional Pad: Alternative control method with directional buttons
Emergency Stop: Instant stop functionality for safety
Custom Commands: Programmable command buttons for specific robot actions
🔌 Multi-Platform Connectivity
WebSocket Integration: Real-time communication with Python/ESP32 robot servers
Multiple Robot Profiles: Support for Raspberry Pi, ESP32, and custom robot configurations
Connection Management: Automatic reconnection and connection status monitoring
IP History: Remember and quick-connect to previously used robot IPs
📊 Real-time Monitoring
Telemetry Display: Live robot status and sensor data
Connection Status: Visual indicators for connection health
Command Logging: Track and review sent commands
Error Handling: Comprehensive error reporting and recovery
🎨 Modern UI/UX
Dark/Light Mode: Automatic theme switching based on system preferences
Haptic Feedback: Tactile responses for better user experience
Smooth Animations: Fluid transitions and visual feedback
Responsive Design: Optimized for various screen sizes and orientations
🔧 Advanced Features
Recording Control: Start/stop robot movement recording
Mode Switching: Toggle between manual and autonomous modes
Screen Orientation Lock: Portrait mode optimization
Offline Capability: Works without internet connection
🚀 Quick Start
Prerequisites
Node.js (v18 or later)
npm or yarn
Expo CLI (npm install -g @expo/cli)
iOS Simulator (for iOS development) or Android Studio (for Android development)
Installation
Clone the repository

git clone https://github.com/Crop-Ally/CropAlly-Mobile.git
cd CropAlly-Mobile
Install dependencies

npm install
# or
yarn install
Start the development server

npm start
# or
yarn start
Run on device/simulator

# For iOS
npm run ios

# For Android
npm run android

# For web
npm run web
🔧 Configuration
Robot Server Setup
The app connects to robot servers via WebSocket. Supported server types:

Raspberry Pi Robot
Port: 5000
Features: Camera, recording, autonomous mode, telemetry
Protocol: WebSocket with JSON messages
ESP32 Robot
Port: 81
Features: Basic movement control
Protocol: WebSocket with simplified commands
Environment Variables
Create a .env file in the root directory:

EXPO_PUBLIC_SOCKET_URL=ws://your-robot-ip:port
Default Connection Settings
Default IP: 172.20.10.8:5000
Connection Timeout: 10 seconds
Reconnect Interval: 5 seconds
Heartbeat Interval: 5 seconds
📱 App Structure
CropAlly-Mobile/
├── app/                    # Expo Router app directory
│   ├── (controller)/      # Main robot control screens
│   │   ├── index.tsx      # Welcome/connection screen
│   │   ├── control.tsx    # Main control interface
│   │   ├── settings.tsx   # App settings
│   │   └── help.tsx       # Help documentation
│   └── (app)/             # Additional app screens
├── components/            # Reusable UI components
│   ├── robot-control/     # Robot-specific components
│   ├── ui/               # General UI components
│   └── ...               # Other component files
├── constants/            # App constants and configurations
├── context/              # React Context providers
├── hooks/                # Custom React hooks
├── lib/                  # Utility libraries
└── assets/               # Images, fonts, and other assets
🔌 WebSocket Protocol
The app communicates with robot servers using standardized JSON messages:

Movement Commands
{
  "type": "tank",
  "left": 0.5,    // Left motor speed (-1 to 1)
  "right": -0.3   // Right motor speed (-1 to 1)
}
Control Commands
// Emergency stop
{ "type": "stop" }

// Recording control
{ "type": "record", "action": "start" }
{ "type": "record", "action": "stop" }

// Mode switching
{ "type": "mode", "mode": "AUTONOMOUS" }
{ "type": "mode", "mode": "MANUAL" }
🛠️ Development
Available Scripts
npm start          # Start Expo development server
npm run android    # Run on Android device/emulator
npm run ios        # Run on iOS device/simulator
npm run web        # Run in web browser
npm run lint       # Run ESLint and Prettier checks
npm run format     # Format code with ESLint and Prettier
npm run prebuild   # Prepare for native build
Code Style
The project uses:

ESLint for code linting
Prettier for code formatting
TypeScript for type safety
NativeWind for styling (Tailwind CSS for React Native)
Testing
Test files are included for WebSocket functionality:

test-websocket.js - Basic WebSocket connection testing
test-websocket-correct.js - Corrected WebSocket testing
test-esp32-connection.js - ESP32-specific connection testing
test-message-formats.js - Message format validation
📋 Requirements
Dependencies
React Native: 0.79.2
Expo: ~53.0.5
TypeScript: ~5.8.3
NativeWind: ^4.1.23
React Navigation: ^7.1.6
Supported Platforms
✅ iOS (iPhone & iPad)
✅ Android
✅ Web (limited functionality)
🤝 Contributing
We welcome contributions! Please follow these steps:

Fork the repository
Create a feature branch (git checkout -b feature/amazing-feature)
Commit your changes (git commit -m 'Add amazing feature')
Push to the branch (git push origin feature/amazing-feature)
Open a Pull Request
Development Guidelines
Follow TypeScript best practices
Use functional components with hooks
Implement proper error handling
Add appropriate comments and documentation
Test on both iOS and Android platforms
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🆘 Support
Troubleshooting
Connection Issues
Verify robot server is running
Check IP address and port configuration
Ensure devices are on the same network
Check firewall settings
Build Issues
Clear Expo cache: expo start -c
Reset Metro cache: npx react-native start --reset-cache
Reinstall dependencies: rm -rf node_modules && npm install
Documentation
WebSocket Integration Guide
Expo Documentation
React Native Documentation
🙏 Acknowledgments
Built with Expo
Styled with NativeWind
Icons from Expo Vector Icons
Animations powered by React Native Reanimated
Made with ❤️ for the agricultural robotics community**
