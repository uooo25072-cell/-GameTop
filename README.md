# GameTop 🎮

منصة احترافية كاملة لشحن الألعاب وبطاقات الهدايا، مبنية بأحدث إصدارات React 18 + Vite 5 و Firebase.

![GameTop](https://img.shields.io/badge/React-18-61dafb)
![Vite](https://img.shields.io/badge/Vite-5-646cff)
![Firebase](https://img.shields.io/badge/Firebase-10-ffca28)
![License](https://img.shields.io/badge/License-MIT-green)

## ✨ المميزات

- ✅ **React 18 + Vite 5** — أحدث إصدارات مستقرة وأداء فائق
- ✅ **Firebase Authentication** — تسجيل دخول/إنشاء حساب/استعادة كلمة المرور
- ✅ **Firebase Firestore** — قاعدة بيانات NoSQL في الوقت الفعلي
- ✅ **Firebase Storage** — رفع صور إثبات الدفع
- ✅ **Firebase Hosting** جاهز للنشر بأمر واحد
- ✅ **React Router 6** للتنقل
- ✅ **Responsive 100%** — يعمل على جميع الأجهزة
- ✅ **SEO جاهز** — meta tags, sitemap, robots, Open Graph
- ✅ **Dark Mode** بتصميم Gaming احترافي
- ✅ **Neon Glow + Animations**
- ✅ **لوحة إدارة كاملة** محمية بصلاحيات Admin
- ✅ **بحث وفلترة وترتيب** للألعاب
- ✅ **حفظ أكثر من UID** للمستخدم
- ✅ **رفع إثبات الدفع** بـ Firebase Storage
- ✅ **Toast Notifications**
- ✅ **Loading Screens**
- ✅ **Firebase Security Rules** آمنة
- ✅ **بيانات ديناميكية بالكامل** — يمكن تعديلها من لوحة الإدارة

## 📦 الألعاب المدعومة

- PUBG Mobile
- Free Fire
- Roblox Gift Cards
- Google Play Gift Cards
- Apple Gift Cards
- Xbox Gift Cards
- Steam Gift Cards

## 💳 طرق الدفع

- Vodafone Cash
- InstaPay
- USDT (BEP20)
- TON

## 🚀 خطوات التشغيل

### 1. تثبيت الحزم

```bash
npm install
```

### 2. إعداد Firebase

1. أنشئ مشروع Firebase جديد من [Firebase Console](https://console.firebase.google.com)
2. فعّل **Authentication** (Email/Password)
3. أنشئ قاعدة بيانات **Firestore** (Production mode)
4. فعّل **Storage**
5. من **Project Settings → General → Your apps** أنشئ تطبيق Web وانسخ الـ config
6. انسخ ملف البيئة:
   ```bash
   cp .env.example .env
   ```
7. املأ المفاتيح في `.env`:
   ```
   VITE_FIREBASE_API_KEY=...
   VITE_FIREBASE_AUTH_DOMAIN=...
   VITE_FIREBASE_PROJECT_ID=...
   VITE_FIREBASE_STORAGE_BUCKET=...
   VITE_FIREBASE_MESSAGING_SENDER_ID=...
   VITE_FIREBASE_APP_ID=...
   ```

### 3. نشر قواعد الأمان

```bash
firebase login
firebase use --add   # اختر مشروعك
firebase deploy --only firestore:rules,firestore:indexes,storage
```

### 4. تشغيل المشروع محلياً

```bash
npm run dev
```

الموقع سيفتح على [http://localhost:5173](http://localhost:5173)

### 5. بناء نسخة الإنتاج

```bash
npm run build
```

الملفات النهائية ستكون في مجلد `dist/`.

### 6. النشر على Firebase Hosting

```bash
firebase deploy --only hosting
```

## 👤 إنشاء حساب المدير

الحساب الأول الذي يُسجل بالإعدادات `VITE_ADMIN_EMAIL` (الافتراضي `admin@gametop.com`) يصبح مديراً تلقائياً. ثم يمكنك:
- الدخول من `/auth/login`
- ستظهر لك لوحة الإدارة في القائمة
- افتح `/admin`

## 📂 هيكل المشروع

```
gametop/
├── public/
│   ├── favicon.svg
│   ├── manifest.json
│   ├── robots.txt
│   ├── sitemap.xml
│   └── images/
│       ├── games/      # صور الألعاب (SVG)
│       └── banners/    # بانرات الألعاب
├── src/
│   ├── assets/
│   ├── components/     # Header, Footer, Layouts, Modal, ...
│   ├── contexts/       # AuthContext, DataContext
│   ├── data/           # seed.js (بيانات افتراضية)
│   ├── hooks/
│   ├── pages/
│   │   ├── auth/       # Login, Register, Forgot Password
│   │   ├── account/    # Profile, Orders, UIDs, Notifications
│   │   ├── games/      # GamePage, Payment
│   │   └── admin/      # Dashboard, Users, Games, Packages, ...
│   ├── services/       # firebase, backup, reports
│   ├── styles/         # CSS files
│   ├── utils/          # format helpers
│   ├── App.jsx
│   └── main.jsx
├── .env.example
├── .gitignore
├── firestore.rules     # قواعد أمان Firestore
├── firestore.indexes.json
├── storage.rules       # قواعد أمان Storage
├── firebase.json       # إعدادات Firebase Hosting
├── index.html
├── package.json
├── postcss.config.js
├── vite.config.js
└── README.md
```

## 🎨 التصميم

- **اللون الأساسي:** أسود (#0a0e1a)
- **اللون الثانوي:** Neon Blue (#00e5ff)
- **التأثيرات:** Glow, Animations, Floating, Grid
- **الخطوط:** Cairo (عربي) + Orbitron (إنجليزي/ألعاب)

## 🔐 الأمان

- Firebase Authentication للعمليات الحساسة
- Firestore Security Rules مفصلة لكل مجموعة
- Storage Rules تحد من نوع وحجم الملفات
- الأدوار محصورة بالـ Admin فقط

## 📊 لوحة الإدارة

- إدارة المستخدمين (ترقية/إزالة إشراف)
- إدارة الألعاب (إضافة/تعديل/حذف)
- إدارة الباقات (إضافة/تعديل/حذف)
- إدارة الطلبات (قبول/رفض/إكمال)
- إدارة وسائل الدفع (إضافة/تعديل/حذف)
- إرسال إشعارات لمستخدم أو للجميع
- إدارة تقييمات العملاء
- إعدادات الموقع
- سجل نشاط كامل
- نسخ احتياطي (JSON)
- تقارير وإحصائيات (الإيرادات، متوسط الطلب، توزيع الحالات)

## 📱 Responsive

- Mobile (320px+)
- Tablet (768px+)
- Desktop (1024px+)
- Large screens (1440px+)

## 🌐 SEO

- Meta tags كاملة
- Open Graph
- Twitter Cards
- Sitemap.xml
- Robots.txt
- Manifest.json
- HelmetProvider لإدارة ديناميكية

## 🛠️ أوامر npm

```bash
npm run dev      # تشغيل وضع التطوير
npm run build    # بناء للإنتاج
npm run preview  # معاينة البناء
npm run lint     # فحص الكود
```

## 📝 الترخيص

هذا المشروع مرخص بموجب MIT License.

## 📞 الدعم

- 📧 Email: svgg2449@gmail.com
- 💬 WhatsApp: 01557535435

---

صُنع بـ ❤️ للاعبين العرب