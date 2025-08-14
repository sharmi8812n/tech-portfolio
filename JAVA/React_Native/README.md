# React Native Android App

This project is a React Native app targeting Android devices and emulators.

## 1. Configuration

### Prerequisites

- **Node.js**: Install from [https://nodejs.org/](https://nodejs.org/)
- **Yarn or npm**: Package managers (npm comes with Node.js)
- **React Native CLI**: Install globally

npm install -g react-native-cli
Android Setup

Install Android Studio from https://developer.android.com/studio

Open Android Studio and install:

Android SDK

SDK Platform

Android Emulator

Open AVD Manager in Android Studio and create a new Android Virtual Device (emulator).

Set environment variables in your shell config file (~/.bashrc, ~/.zshrc, etc.):

export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools


Note: Adjust $ANDROID_HOME path if you are on Linux or Windows.

2. Running Steps
Install Dependencies
Clone the repo and install packages:
git clone https://github.com/yourusername/your-react-native-app.git
cd your-react-native-app
npm install
# or
yarn install

Start Android Emulator
Open Android Studio
Open AVD Manager
Start your preferred Android Virtual Device
Run React Native App on Android Emulator

Start Metro Bundler:
npx react-native start


In a new terminal window, run:
npx react-native run-android

This will build your app, install it on the running emulator, and launch it.

Troubleshooting
If the emulator does not start automatically, start it manually via Android Studio before running run-android.
Verify your device is connected or emulator is running with:
adb devices


To clear cache if you encounter issues:
npx react-native start --reset-cache
