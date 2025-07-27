# 🔐 Entity: Permission (سطوح دسترسی)

## 🎯 هدف
تعریف سطوح دسترسی برای کنترل عملیات مختلف روی ماژول‌های مختلف سیستم.  
هر Permission نشان‌دهنده یک عملیات خاص روی یک ماژول مشخص است (مثلاً: ایجاد نامه، حذف کاربر، چاپ گزارش).

---

## 🧱 فیلدهای اصلی

| فیلد              | نوع        | توضیح |
|-------------------|------------|--------|
| `Id`              | `Guid`     | شناسه یکتا |
| `Code`            | `string`   | کد یونیک (مثلاً `DOC_CREATE`) |
| `Name`            | `string`   | عنوان نمایشی (مثلاً "ایجاد نامه") |
| `Module`          | `string`   | نام ماژول مربوطه (مثلاً `Letter`, `User`, `Report`) |
| `Action`          | `string`   | نوع عملیات (مثلاً `Create`, `Edit`, `Delete`, `View`, `Print`) |
| `Description`     | `string?`  | توضیح اختیاری |
| `CreatedAt`       | `DateTime` | تاریخ ایجاد |
| `IsSystemPermission` | `bool`  | آیا این Permission سیستمی و غیرقابل حذف است؟ |

---

## 🔄 ارتباطات

- `RolePermission`: ارتباط چند به چند با Role
- `UserPermissionOverride` (آینده): دسترسی خاص برای کاربران خاص

---

## 📌 نمونه Permissionها

| Code         | Module  | Action  | Name             |
|--------------|---------|---------|------------------|
| `DOC_CREATE` | Letter  | Create  | ایجاد نامه       |
| `DOC_EDIT`   | Letter  | Edit    | ویرایش نامه      |
| `DOC_VIEW`   | Letter  | View    | مشاهده نامه       |
| `USR_MANAGE` | User    | Manage  | مدیریت کاربران    |
| `REP_EXPORT` | Report  | Export  | خروجی گزارش       |

---

## 🧠 توسعه آینده (Future-Oriented Notes)

| ویژگی               | توضیح |
|---------------------|-------|
| `PermissionCategory` | گروه‌بندی مجوزها (مثلاً: دسترسی‌های مرتبط با منابع انسانی) |
| `DependsOn`         | وابستگی به سایر مجوزها (مثلاً: برای حذف باید مجوز مشاهده هم داشته باشد) |
| `UIVisibility`      | نمایش یا عدم نمایش گزینه‌ها در UI بر اساس مجوز |
| `PermissionLevel`   | سطح‌بندی مجوزها (مثلاً: `Full`, `Partial`, `ReadOnly`) |

---



