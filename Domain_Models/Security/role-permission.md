# 🔗 Entity: RolePermission (رابط نقش و مجوز)

## 🎯 هدف
تعریف رابطه‌ی چند به چند بین نقش‌ها (`Role`) و مجوزها (`Permission`).  
هر نقش می‌تواند چندین مجوز داشته باشد، و هر مجوز می‌تواند به چند نقش تخصیص یابد.

---

## 🧱 فیلدهای اصلی

| فیلد              | نوع        | توضیح |
|-------------------|------------|--------|
| `Id`              | `Guid`     | شناسه یکتا |
| `RoleId`          | `Guid`     | شناسه نقش (FK → Role.Id) |
| `PermissionId`    | `Guid`     | شناسه مجوز (FK → Permission.Id) |
| `GrantedAt`       | `DateTime` | تاریخ اعطای دسترسی |
| `GrantedByUserId` | `Guid?`    | کاربری که این دسترسی را ایجاد کرده است (اختیاری) |

---

## 🔄 ارتباطات

- `RolePermission → Role` (Many-to-One)
- `RolePermission → Permission` (Many-to-One)
- `User` (در آینده برای `GrantedByUserId`)

---

## 🧠 توسعه آینده (Future-Oriented Notes)

| ویژگی | توضیح |
|--------|--------|
| `IsOverridden` | اگر نقش خاصی دسترسی متفاوتی نسبت به حالت پیش‌فرض داشته باشد |
| `ValidUntil` | تاریخ انقضا برای دسترسی موقت |
| `ContextualLimitations` | شرایط خاص (مثلاً فقط برای یک سازمان یا فرم خاص) |

---

## 📁 محل ذخیره‌سازی

