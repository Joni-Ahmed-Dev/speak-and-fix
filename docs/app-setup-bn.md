# Speak & Fix: APK বানানোর ধাপ (Capacitor)

## আগে জেনে রাখুন
- আপনার iMac (Late 2013, macOS Monterey) এ Android Studio ধীর চলতে পারে। সহজ বিকল্প নিচে "পথ ২" এ আছে।
- নতুন "রেকর্ড মোড" WebView-তে চলে। পুরনো "Chrome ভয়েস" মোড অ্যাপে চলবে না।

## পথ ১: Capacitor + Android Studio
1. Node.js ইনস্টল করুন (nodejs.org, LTS)।
2. টার্মিনালে:
   ```
   mkdir speak-fix-app && cd speak-fix-app
   npm init -y
   npm i @capacitor/core @capacitor/cli @capacitor/android
   npx cap init "Speak & Fix" com.aminul.speakfix --web-dir=www
   mkdir www
   ```
3. `index.html`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png` ফাইলগুলো `www` ফোল্ডারে রাখুন।
4. `npx cap add android`
5. `android/app/src/main/AndroidManifest.xml` এ `<manifest>` ট্যাগের ভেতরে যোগ করুন:
   ```
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   ```
6. `npx cap sync` তারপর `npx cap open android`। Android Studio-তে Build > Build APK।
7. পরে `index.html` বদলালে: নতুন ফাইল `www` তে কপি করে `npx cap sync`, তারপর আবার বিল্ড।

## পথ ২: সহজ বিকল্প (PWABuilder)
1. `index.html`, `sw.js`, `manifest.webmanifest` ও দুটো আইকন একটা HTTPS সাইটে (GitHub Pages) `/speak-and-fix/` পাথে রাখুন।
2. pwabuilder.com এ সেই লিংক দিয়ে Android প্যাকেজ বানান।
3. এই পথে অ্যাপ Chrome-এর ইঞ্জিনে চলে, তাই ভয়েসের সমস্যা কম হয়। আপডেটও সাইটে ফাইল বদলালেই আসে।

## ওয়েবসাইটে আপডেট দেওয়ার সময়
`sw.js` এ ক্যাশ নাম `speak-and-fix-v2` করেছি। এরপর ফাইল বদলালে প্রতিবার এই সংখ্যা বাড়ান (v3, v4…), নইলে ফোনে পুরনো ভার্সন দেখাবে।
