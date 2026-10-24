# أرشيف أبو ياسر — النسخة المشتركة (claude.ai Artifact)

صفحة HTML واحدة: `abu-yaser-online.html`
منشورة كـ Artifact على: https://claude.ai/artifact/VR9XPCZuezjuird6Sdxz5h

## مهم قبل التعديل
- الصفحة تعمل **داخل claude.ai فقط**، لأنها تعتمد على `window.claude.use(...)` (قاعدة البيانات، رفع الملفات، المستخدم، التنزيل).
  إذا فُتحت مباشرة في المتصفح تظهر رسالة «يعمل من داخل claude.ai فقط».
- الملف لا يحتوي على `<html>/<head>/<body>`؛ منصة Artifact تضيفها عند النشر.
- لإعادة النشر على نفس الرابط من Claude Code: استخدم أداة Artifact مع `url` أعلاه (اقرأ الـ artifact أولاً)، وأعطِ الملف المحدّث.

## القدرات المعلنة (capabilities) — يجب الإبقاء عليها عند النشر
```json
{
  "db": { "rules": [
    { "path": "", "read": "interact", "write": "interact" },
    { "path": "logins", "read": "interact", "write": "owner" }
  ]},
  "user": { "scopes": ["profile"] },
  "assets": {},
  "downloads": true
}
```
- لا يقرأ البيانات إلا صاحب الأرشيف ومن دُعي بالبريد بصلاحية Editor (زوار الرابط العام لا يرون شيئاً).
- حسابات الدخول (`logins`) لا يعدّلها إلا صاحب الأرشيف.

## نموذج البيانات (db)
- `members/<id>`: name, relation, family, birthDate (YYYY-MM-DD), phone, notes, photo (asset id), createdAt, createdBy, createdByAcct, updatedAt, updatedBy
- `docs/<id>`: memberId, type (passport|cpr|license|vehicle|birth|edu|insurance|property|other), title, number, issueDate, expiryDate, remindDays, notes, files:[{id (asset id), name, type}], createdAt, createdBy, updatedAt, updatedBy
- `settings/main`: remindDays (المدة الافتراضية للتنبيه)
- `logins/<'u'+sha256('abu-yaser:'+username)[0:32]>`: username, salt, hash (PBKDF2-SHA256, 150000 تكرار), scope ('all'|'some'), memberIds[], createdAt, createdBy
- الملفات والصور في Assets، وتُعرض من `/_blob/<asset id>`.

## ملاحظات
- شاشة اليوزر/الباسوورد طبقة عرض إضافية؛ الحماية الفعلية هي دعوة البريد بصلاحية Editor.
- تحديد «من يرى؟» لكل حساب تصفية في الواجهة وليس حماية تقنية.
- الخط: Tajawal من Google Fonts، والاتجاه RTL.
