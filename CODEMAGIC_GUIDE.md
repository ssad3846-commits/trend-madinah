# دليل نشر التطبيق عبر Codemagic

## الخطوة 1: إنشاء حساب Codemagic

1. اذهب إلى [codemagic.io](https://codemagic.io)
2. سجل الدخول باستخدام GitHub أو GitLab أو Bitbucket
3. الحساب المجاني يمنحك 500 دقيقة بناء شهرياً

---

## الخطوة 2: رفع المشروع إلى GitHub

إذا لم يكن مشروعك على GitHub:

1. أنشئ مستودع جديد على GitHub
2. ارفع المشروع:
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/trend-madinah.git
git push -u origin main
```

---

## الخطوة 3: ربط المشروع بـ Codemagic

1. في Codemagic، اضغط **"Add application"**
2. اختر **GitHub** واربط حسابك
3. اختر مستودع `trend-madinah`
4. Codemagic سيكتشف ملف `codemagic.yaml` تلقائياً

---

## الخطوة 4: إعداد شهادات Apple

### أ) ربط حساب Apple Developer:

1. في Codemagic، اذهب إلى **Settings → Integrations**
2. اضغط **"Connect"** بجانب App Store Connect
3. أنشئ **App Store Connect API Key**:
   - اذهب إلى [App Store Connect](https://appstoreconnect.apple.com)
   - Users and Access → Keys → "+"
   - اختر **Admin** role
   - حمّل الملف (.p8)
4. أدخل المعلومات في Codemagic:
   - Issuer ID
   - Key ID  
   - Private Key (.p8 file)

### ب) إنشاء الشهادات تلقائياً:

1. في إعدادات التطبيق على Codemagic
2. اذهب إلى **Code signing**
3. اختر **Automatic** - Codemagic سينشئ الشهادات تلقائياً!

---

## الخطوة 5: إنشاء التطبيق في App Store Connect

1. اذهب إلى [App Store Connect](https://appstoreconnect.apple.com)
2. **My Apps** → **"+"** → **New App**
3. أدخل المعلومات:
   - **Platform**: iOS
   - **Name**: ترند المدينة
   - **Primary Language**: Arabic
   - **Bundle ID**: com.saad.trendmadinah
   - **SKU**: trendmadinah2024

---

## الخطوة 6: بدء البناء

1. في Codemagic، اضغط **"Start new build"**
2. اختر **ios-capacitor** workflow
3. اضغط **"Start new build"**
4. انتظر (10-20 دقيقة)

---

## الخطوة 7: النتيجة

بعد نجاح البناء:
- التطبيق يُرفع تلقائياً إلى **TestFlight**
- يمكنك اختباره على جهازك
- بعد الاختبار، ارفعه للـ App Store من App Store Connect

---

## معلومات App Store المطلوبة

### وصف التطبيق:
```
ترند المدينة - منصتك للتواصل مع مجتمعك في المملكة العربية السعودية.

المميزات:
• تابع أخبار منطقتك والترندات المحلية
• شاهد البث المباشر من الحرمين الشريفين
• استمع للإذاعات السعودية
• تواصل مع القريبين منك
• اطرح أسئلتك واحصل على إجابات
```

### الكلمات المفتاحية:
```
ترند، المدينة، السعودية، أخبار، تواصل، مجتمع، تويتر، اجتماعي
```

### لقطات الشاشة:
- ستحتاج 3-5 لقطات شاشة لكل حجم جهاز
- التقطها من المتصفح أو المحاكي

### متطلبات أخرى:
- رابط سياسة الخصوصية (أنشئ صفحة بسيطة)
- رابط الدعم (بريد إلكتروني)
- التصنيف العمري: 4+

---

## استكشاف الأخطاء

### خطأ في الشهادات:
- تأكد من صحة Bundle ID
- جرب إعادة إنشاء الشهادات من Codemagic

### خطأ في البناء:
- راجع الـ logs في Codemagic
- تأكد من نجاح `npm run build` محلياً

### رفض من Apple:
- اقرأ سبب الرفض بعناية
- غالباً يتعلق بالمحتوى أو الخصوصية

---

## روابط مفيدة

- [Codemagic Docs](https://docs.codemagic.io)
- [Capacitor iOS Docs](https://capacitorjs.com/docs/ios)
- [App Store Connect](https://appstoreconnect.apple.com)
- [Apple Developer](https://developer.apple.com)
