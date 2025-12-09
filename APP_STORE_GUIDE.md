# دليل نشر التطبيق على App Store

## المتطلبات الأساسية

### 1. حساب Apple Developer
- اشترك في [Apple Developer Program](https://developer.apple.com/programs/)
- التكلفة: 99$ سنوياً
- يستغرق التفعيل 24-48 ساعة

### 2. جهاز Mac
- يجب وجود Mac لبناء التطبيق
- macOS Ventura أو أحدث
- Xcode 15 أو أحدث (مجاني من App Store)

### 3. CocoaPods
```bash
sudo gem install cocoapods
```

---

## خطوات البناء والنشر

### الخطوة 1: نقل مجلد iOS إلى Mac
انقل مجلد `ios` من المشروع إلى جهاز Mac

### الخطوة 2: تثبيت Dependencies
```bash
cd ios/App
pod install
```

### الخطوة 3: فتح المشروع في Xcode
```bash
open App.xcworkspace
```

### الخطوة 4: إعداد التوقيع (Signing)
1. افتح Xcode
2. اختر Target "App"
3. اذهب إلى "Signing & Capabilities"
4. اختر Team (حسابك Apple Developer)
5. تأكد من صحة Bundle Identifier: `com.saad.trendmadinah`

### الخطوة 5: إضافة الأيقونات
1. افتح `Assets.xcassets` في Xcode
2. اسحب أيقونة التطبيق (1024x1024) إلى AppIcon
3. Xcode سيُنشئ الأحجام المختلفة تلقائياً

### الخطوة 6: بناء التطبيق
1. اختر "Any iOS Device" كـ Build Target
2. اضغط Product → Archive
3. انتظر انتهاء البناء

### الخطوة 7: رفع إلى App Store Connect
1. بعد Archive، اضغط "Distribute App"
2. اختر "App Store Connect"
3. اتبع الخطوات لرفع التطبيق

---

## إعداد App Store Connect

### 1. إنشاء التطبيق
1. اذهب إلى [App Store Connect](https://appstoreconnect.apple.com)
2. اضغط "My Apps" → "+"
3. أدخل معلومات التطبيق:
   - **Name**: ترند المدينة
   - **Primary Language**: Arabic
   - **Bundle ID**: com.saad.trendmadinah
   - **SKU**: trendmadinah2024

### 2. معلومات التطبيق المطلوبة
- **وصف التطبيق**: 
  ```
  ترند المدينة - منصتك للتواصل مع مجتمعك في المملكة العربية السعودية.
  
  المميزات:
  • تابع أخبار منطقتك والترندات المحلية
  • شاهد البث المباشر من الحرمين الشريفين
  • استمع للإذاعات السعودية
  • تواصل مع القريبين منك
  • اطرح أسئلتك واحصل على إجابات
  ```

- **الكلمات المفتاحية**: ترند، المدينة، السعودية، أخبار، تواصل، مجتمع

- **رابط سياسة الخصوصية**: (مطلوب)

- **رابط الدعم**: (مطلوب)

### 3. لقطات الشاشة المطلوبة
- iPhone 6.7" (1290 × 2796)
- iPhone 6.5" (1242 × 2688)
- iPad Pro 12.9" (2048 × 2732) - اختياري

### 4. التصنيف العمري
- اختر "4+" (مناسب لجميع الأعمار)

---

## Sign in with Apple

### إعداد Return URL للإنتاج
1. اذهب إلى [Apple Developer Console](https://developer.apple.com)
2. Certificates, Identifiers & Profiles → Services IDs
3. اختر Service ID الخاص بك
4. أضف Return URL للإنتاج:
   ```
   https://your-domain.com/api/auth/apple/callback
   ```

---

## تحديث التطبيق

عند تحديث التطبيق، نفذ الخطوات التالية:

```bash
# 1. بناء الويب
npm run build

# 2. نسخ الملفات لـ iOS
npx cap sync ios

# 3. فتح Xcode
npx cap open ios

# 4. زيادة Version و Build Number
# 5. Archive ورفع جديد
```

---

## ملاحظات مهمة

1. **مراجعة Apple**: تستغرق 1-7 أيام عمل
2. **الرفض**: إذا تم رفض التطبيق، ستصلك رسالة بالسبب
3. **TestFlight**: يمكنك اختبار التطبيق داخلياً قبل النشر

---

## الدعم

للمساعدة في أي خطوة، راجع:
- [Capacitor iOS Docs](https://capacitorjs.com/docs/ios)
- [App Store Connect Help](https://developer.apple.com/help/app-store-connect/)
