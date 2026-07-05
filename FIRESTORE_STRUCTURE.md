# GameTop - هيكل قاعدة بيانات Firestore

هذا الملف يوضح هيكل قاعدة البيانات الموصى به لتشغيل منصة GameTop بشكل كامل.

## المجموعات (Collections)

### 1. `users/{uid}`
```js
{
  uid: string,
  name: string,
  email: string,
  phone: string,
  role: 'user' | 'admin',
  savedUIDs: [
    {
      id: 'uid_xxxxx',
      gameId: 'pubg',
      label: 'حسابي الأساسي',
      value: '1234567890',
      createdAt: number
    }
  ],
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### 2. `games/{gameId}`
```js
{
  id: 'pubg',
  slug: 'pubg',
  name: 'PUBG Mobile',
  category: 'topup' | 'battle-royale' | 'gift-card',
  color: '#ffb300',
  shortDescription: '...',
  longDescription: '...',
  image: '/images/games/pubg.svg',
  banner: '/images/banners/pubg.svg',
  accountType: 'uid' | 'email',
  accountLabel: 'UID اللاعب',
  accountPlaceholder: 'أدخل UID',
  popular: boolean,
  bestseller: boolean,
  active: boolean,
  order: number,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### 3. `packages/{pkgId}`
```js
{
  id: 'pubg_325',
  gameId: 'pubg',
  name: '325 UC',
  amount: number,
  price: number,
  popular: boolean,
  active: boolean,
  stock: number | null,    // null = غير محدود
  order: number,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### 4. `paymentMethods/{pmId}`
```js
{
  id: 'pm_vodafone',
  name: 'Vodafone Cash',
  type: 'vodafone' | 'instapay' | 'usdt' | 'ton' | 'bank',
  accountNumber: '01060932168',
  accountName: 'Vodafone Cash',
  instructions: '...',
  requiresPhone: boolean,
  requiresWallet: boolean,
  requiresReference: boolean,
  active: boolean,
  order: number
}
```

### 5. `orders/{orderId}` (auto-id)
```js
{
  orderId: 'GT-XXXXXX-XXXX',
  userId: string,
  userEmail: string,
  userName: string,
  gameId: 'pubg',
  gameName: 'PUBG Mobile',
  gameSlug: 'pubg',
  packageId: 'pubg_325',
  packageName: '325 UC',
  packageAmount: 325,
  packagePrice: 4.79,
  accountType: 'uid' | 'email',
  accountValue: '1234567890',
  paymentMethodId: 'pm_vodafone',
  paymentMethodName: 'Vodafone Cash',
  amount: 4.79,
  currency: 'USD',
  status: 'awaiting_payment' | 'pending_review' | 'approved' | 'rejected' | 'completed' | 'cancelled',
  promoCode: '',
  paymentReference: '',
  paymentSender: '',
  proofUrl: 'https://firebasestorage...',
  proofPath: 'proofs/...',
  rejectReason: '',
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### 6. `notifications/{notifId}`
```js
{
  userId: string | 'all',
  userEmail: string,
  title: '...',
  message: '...',
  type: 'info' | 'success' | 'warning' | 'danger',
  read: boolean,
  createdAt: timestamp
}
```

### 7. `reviews/{reviewId}`
```js
{
  userId: string,
  userName: string,
  rating: number (1-5),
  comment: string,
  approved: boolean,
  createdAt: timestamp
}
```

### 8. `activity/{activityId}`
```js
{
  type: string,            // order_create, admin_game_upsert, ...
  message: string,
  meta: object,
  userId: string,
  userEmail: string,
  createdAt: timestamp
}
```

### 9. `settings/site` (single doc)
```js
{
  siteName: 'GameTop',
  siteDescription: '...',
  whatsappNumber: '201557535435',
  contactEmail: 'svgg2449@gmail.com',
  currency: 'USD',
  maintenance: false,
  bestSellers: ['pubg', 'free-fire', 'roblox']
}
```

## Firebase Storage

- `proofs/{orderId}/{filename}` — صور إثبات الدفع (5MB max, صور فقط)

## الصلاحيات

راجع `firestore.rules` و `storage.rules` لمعرفة قواعد الأمان الكاملة.

## تهيئة قاعدة البيانات تلقائياً

عند فتح الموقع لأول مرة (بعد إعداد Firebase)، يقوم `DataProvider` تلقائياً بـ:
- إنشاء مستند الإعدادات إذا لم يكن موجوداً
- إضافة الألعاب الافتراضية من `seed.js`
- إضافة الباقات الافتراضية
- إضافة وسائل الدفع الافتراضية

يمكنك تعديل كل ذلك لاحقاً من لوحة الإدارة دون لمس الكود.