# 🔧 APK 安裝問題偵錯指南

## 📱 大學生小助手 - 安裝問題解決方案

**日期**: 2025年6月7日  
**狀態**: 🔍 **偵錯進行中**  
**問題**: APK 安裝失敗  

---

## 🎯 已修復的建置問題

### ✅ **1. Gradle 語法修復**
- 修復 `buildTypes` 區塊格式錯誤
- 修復 `kotlinOptions` 和 `buildFeatures` 間距問題
- 修復 `androidTestImplementation` 行格式

### ✅ **2. 檔案完整性檢查**
- ✅ `CollegeAssistantApplication.kt` - 正確配置 Hilt
- ✅ `MainActivity.kt` - 正確配置 Compose
- ✅ `AndroidManifest.xml` - 配置正確

---

## 🚨 常見安裝失敗原因及解決方案

### **原因 1: 簽署問題**
```powershell
# 檢查 APK 簽署狀態
keytool -printcert -jarfile "app-debug.apk"
```

**解決方案**: Debug APK 使用系統預設簽署

### **原因 2: 應用程式 ID 衝突**
- **應用程式 ID**: `com.collegeassistant.app`
- **解決方案**: 如果裝置上已有相同 ID 的應用程式，請先解除安裝

### **原因 3: 最低 SDK 版本不符**
- **最低版本**: Android 7.0 (API 24)
- **目標版本**: Android 14 (API 34)
- **解決方案**: 確認裝置 Android 版本 ≥ 7.0

### **原因 4: 儲存空間不足**
- **APK 大小**: 約 15-25 MB
- **解決方案**: 確保裝置有足夠空間

### **原因 5: 未知來源設定**
**解決方案**:
1. 設定 → 安全性 → 允許來自此來源的應用程式
2. 或使用 ADB 安裝

---

## 🛠️ 安裝方法 (依優先順序)

### **方法 1: ADB 安裝 (推薦)**
```powershell
# 啟用開發者選項和 USB 偵錯
adb devices
adb install -r "c:\Users\user\Desktop\大學生小助手\app\build\outputs\apk\debug\app-debug.apk"
```

### **方法 2: Gradle 直接安裝**
```powershell
cd "c:\Users\user\Desktop\大學生小助手"
.\gradlew.bat installDebug
```

### **方法 3: 手動安裝**
1. 啟用「未知來源」
2. 將 APK 複製到裝置
3. 點擊安裝

---

## 🔍 進階偵錯命令

### **檢查建置狀態**
```powershell
.\gradlew.bat assembleDebug --info --stacktrace
```

### **檢查相依性**
```powershell
.\gradlew.bat app:dependencies
```

### **檢查 APK 內容**
```powershell
# 檢查 APK 結構
unzip -l "app-debug.apk"
```

### **檢查裝置相容性**
```powershell
adb shell getprop ro.build.version.sdk
adb shell pm list packages | findstr collegeassistant
```

---

## 🎯 如果仍無法安裝

### **生成發佈版本 APK**
```powershell
.\gradlew.bat assembleRelease
```

### **檢查建置日誌**
```powershell
.\gradlew.bat assembleDebug --debug > build.log 2>&1
```

### **重新生成金鑰庫**
如果需要自定義簽署:
```powershell
keytool -genkey -v -keystore college-assistant.jks -keyalg RSA -keysize 2048 -validity 10000 -alias college-assistant
```

---

## 📋 檢查清單

- [ ] APK 檔案已生成
- [ ] 裝置 Android 版本 ≥ 7.0
- [ ] 儲存空間充足 (>50MB)
- [ ] 已啟用「未知來源」或「開發者選項」
- [ ] 沒有相同應用程式 ID 的應用程式
- [ ] 使用 ADB 安裝

---

## 🏁 預期結果

APK 成功安裝後，您應該看到:
- 📱 「大學生小助手」應用程式圖示
- 🌞 固定淺色主題介面
- 🏠 主畫面載入正常
- ✅ 各功能模組可正常使用

---

*如果問題持續存在，請檢查建置日誌或嘗試在不同裝置上安裝* 🔧
