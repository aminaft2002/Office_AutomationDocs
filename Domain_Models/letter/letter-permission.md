
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
