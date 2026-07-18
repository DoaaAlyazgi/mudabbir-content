# كيف تفعّلي المزامنة الحقيقية عبر GitHub

## 1. أنشئي مستودع (Repository) جديد على GitHub
- ممكن يكون **عام (Public)** — أسهل وأسرع، ومحتوى إرشادي عام أصلاً مش سري
- سمّيه مثلاً: `mudabbir-content`

## 2. ارفعي هذا المجلد (`server_content_example`) بالكامل لجذر المستودع
يعني بعد الرفع، شكل المستودع يكون:
```
mudabbir-content/
  manifest.json
  categories.json
  service_items.json
  medical_guides.json
```

## 3. احصلي على الرابط الخام (Raw URL)
افتحي أي ملف بالمستودع على GitHub، اضغطي زر "Raw"، وانسخي الرابط.
شكله بيكون تقريباً:
```
https://raw.githubusercontent.com/USERNAME/mudabbir-content/main/manifest.json
```

## 4. ضعي الرابط الأساسي (بدون اسم الملف) بالتطبيق
افتحي:
```
lib/core/constants/app_constants.dart
```
وعدّلي هذا السطر:
```dart
static const String contentBaseUrl =
    'https://raw.githubusercontent.com/USERNAME/mudabbir-content/main';
```
استبدلي `USERNAME` باسم حسابك الفعلي، و`mudabbir-content` باسم المستودع لو غيرتيه.

## 5. كيف تحدّثي المحتوى مستقبلاً؟
1. عدّلي أي ملف JSON مباشرة على GitHub (أو ارفعي نسخة جديدة)
2. **الأهم:** زيدي رقم `version` بملف `manifest.json` بواحد (مثلاً من 1 لـ 2)
3. هيك التطبيق بيعرف إنه في تحديث جديد ويحمّله تلقائياً أول ما يلاقي إنترنت

⚠️ لو نسيتي تزيدي رقم النسخة، التطبيق رح يعتبر ما في تحديث جديد ولن يحمّل التعديلات!

## ملاحظة عن Google Sheets (لاحقاً)
حالياً التحديث يدوي (تعديل ملفات JSON مباشرة على GitHub).
لاحقاً، ممكن نبني سكربت بسيط (GitHub Action مثلاً) يقرأ من Google Sheets
ويحدّث ملفات JSON هاي تلقائياً — بس هاد يحتاج Google Sheets يكون جاهز وفيه
بيانات فعلية أول، فهو خطوة تالية بعد ما يستقر شكل المحتوى.
