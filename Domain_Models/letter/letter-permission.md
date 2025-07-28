
# 🛡 Entity: LetterPermission (سطح دسترسی به نامه)

## 🎯 هدف
مدل `LetterPermission` مشخص می‌کند که چه کسی (کاربر یا واحد سازمانی) به کدام نامه چه سطحی از دسترسی دارد.

---

## 🧱 فیلدهای اصلی

| فیلد | نوع | توضیح |
|------|------|--------|
| `Id` | `Guid` | شناسه یکتا |
| `LetterId` | `Guid` | شناسه نامه |
| `PermissionType` | `PermissionTargetType` | نوع دسترسی (کاربر، واحد سازمانی) |
| `TargetId` | `Guid` | شناسه کاربر یا واحد (بسته به نوع) |
| `AccessLevel` | `AccessLevelEnum` | سطح دسترسی (نمایش، ویرایش، حذف) |
| `GrantedByUserId` | `Guid` | چه کسی این دسترسی را داده |
| `GrantedAt` | `DateTime` | زمان اعطای دسترسی |


|رابطه|نوع ارتباط|توضیح|
|---|---|---|
|`LetterPermission → Letter`|Many-to-One|این سطح دسترسی به کدام نامه مربوط است|
|`LetterPermission → User`|Many-to-One (اختیاری)|دسترسی برای کاربر خاص|
|`LetterPermission → Unit`|Many-to-One (اختیاری)|یا دسترسی برای یک واحد (گروه) خاص|
|`LetterPermission → PermissionType`|Enum|نوع سطح دسترسی: مشاهده، ویرایش، حذف، ارجاع و...|
|`LetterPermission → GrantedBy`|Many-to-One|کاربری که این دسترسی را ایجاد کرده|
|`LetterPermission → GrantedAt`|DateTime|تاریخ ثبت دسترسی|


## 🧩 وابستگی‌های اصلی

- `Letter` ← برای `LetterId`
    
- `User` ← برای `UserId` (در صورت شخصی بودن دسترسی)
    
- `Unit` ← برای `UnitId` (در صورت گروهی بودن دسترسی)
    
- `PermissionType` ← Enum برای مشخص کردن نوع مجوز
    
- `User` ← برای `GrantedById`
    

---

## 🔸 Enum پیشنهادی برای PermissionType

csharp

CopyEdit

`enum LetterPermissionType {   View,   Edit,   Delete,   Refer,   Comment }`

---

## ⚙️ نکات فنی مهم

- فقط یکی از فیلدهای `UserId` یا `UnitId` باید مقدار داشته باشد (نه هر دو).
    
- در صورت عدم وجود هیچ `LetterPermission`ی برای یک نامه، ممکن است فقط مالک یا فرستنده مجاز به دیدن آن باشد.
    
- این جدول پایه‌ اصلی برای **RBAC یا ABAC** در سطح نامه‌ها خواهد بود.
---
## 📌 نکات طراحی

- `TargetId` می‌تواند شناسه کاربر یا واحد باشد، بسته به مقدار `PermissionType`
    
- در آینده می‌توان دسترسی‌ها را بر اساس نقش‌ها (Role) هم توسعه داد
    
- این مدل به ما اجازه می‌دهد تا به‌صورت جزئی تعیین کنیم چه کسی به چه نامه‌ای چه کاری می‌تواند انجام دهد
    

---

## 🔐 آینده‌نگری

در سیستم‌های Enterprise، مدل دسترسی باید:

- قابل توسعه باشد (برای Role-based Access Control)
    
- امکان audit (ردیابی تغییرات دسترسی) داشته باشد
## 🔸 Enums مورد نیاز

```csharp
enum PermissionTargetType {
  User,
  OrganizationUnit
}

enum AccessLevelEnum {
  ReadOnly,
  ReadWrite,
  FullControl
}
