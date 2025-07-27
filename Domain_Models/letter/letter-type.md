
|فیلد|نوع داده|توضیح|
|---|---|---|
|`id`|UUID|شناسه یکتا|
|`title`|string|عنوان نوع نامه (مثلاً: "صادره"، "وارده"، "داخلی")|
|`description`|string|توضیح اختیاری درباره این نوع نامه|
|`isActive`|boolean|آیا این نوع فعال است یا خیر|
|`isDefault`|boolean|آیا این نوع به‌صورت پیش‌فرض در فرم‌ها استفاده شود؟|
|`createdAt`|datetime|زمان ایجاد|
|`updatedAt`|datetime|زمان آخرین بروزرسانی|

### 🧩 مثال مقادیر اولیه (Seed Data):

[
  {
    "id": "uuid1",
    "title": "نامه صادره",
    "description": "نامه‌هایی که از سازمان خارج می‌شوند",
    "isActive": true,
    "isDefault": false
  },
  {
    "id": "uuid2",
    "title": "نامه وارده",
    "description": "نامه‌هایی که به سازمان وارد شده‌اند",
    "isActive": true,
    "isDefault": false
  },
  {
    "id": "uuid3",
    "title": "نامه داخلی",
    "description": "نامه‌های درون‌سازمانی بین پرسنل",
    "isActive": true,
    "isDefault": true
  }
]


---

### 🔐 محدودیت‌ها و نکات:

- فقط یک `letter-type` می‌تواند `isDefault = true` داشته باشد.
    
- عنوان‌ها باید **منحصر به‌فرد** باشند.
    
- غیرفعال بودن یک نوع باعث عدم نمایش در فرم‌های ثبت می‌شود.