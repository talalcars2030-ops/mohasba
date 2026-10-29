# المحاسبة

تطبيق ويب (PWA) لتسجيل عمليات العملاء وأرصدتهم. يعمل بدون إنترنت ويتزامن مع **Google Sheets** بحساب Google واحد.

## النشر على GitHub Pages
ارفع محتويات المجلد (index.html، config.js، manifest.json، sw.js، icon-192.png، icon-512.png، README.md) إلى المستودع، ثم Settings ← Pages ← main ← /(root).
احذف مجلد `supabase` القديم؛ لم يعد مستخدماً.

## تفعيل تسجيل الدخول بـ Google (مرة واحدة من المطوّر فقط)
1. console.cloud.google.com ← أنشئ مشروعاً.
2. APIs & Services ← Library ← فعّل **Google Sheets API** و **Google Drive API**.
3. OAuth consent screen: النوع External، ثم اجعل الحالة **In production**. الصلاحية المستخدمة (drive.file) غير حساسة فلا تحتاج مراجعة من Google.
4. Credentials ← Create credentials ← OAuth client ID ← Web application.
   Authorized JavaScript origins: `https://talalcars2030-ops.github.io` (بدون المسار).
5. انسخ الـ Client ID إلى `config.js` ثم Commit.

بعدها أي مستخدم يضغط «تسجيل الدخول بحساب Google» فقط.

## كيف تُحفظ البيانات
- محلياً على الجهاز دائماً (تعمل بلا إنترنت)، وتُزامَن مع جدول «المحاسبة - البيانات» الذي ينشئه التطبيق في Drive الخاص بالمستخدم.
- التطبيق لا يرى أي ملف آخر في Drive (صلاحية drive.file).
- المبالغ تُخزَّن كأعداد صحيحة (هللات)، والرصيد يُحسب دائماً من العمليات ولا يُخزَّن.
- العمليات لا تُحذف؛ تُلغى مع سبب ويبقى أثرها في السجل.
- في الجدول ورقة Balances بمعادلات حيّة (SUMIFS)، وكل الأوراق من اليمين لليسار.
