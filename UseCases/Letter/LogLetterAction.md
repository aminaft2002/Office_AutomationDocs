
### 🎯 هدف:

ثبت کلیه عملیات‌های کاربر روی نامه‌ها (مثل ایجاد، ویرایش، حذف، ارسال، ارجاع، مشاهده، بازیابی، بایگانی و...) در جدول `LetterLog` برای مقاصد پیگیری، گزارش‌گیری، و audit trail.

---

### 🧩 پیش‌نیازها:

|شرط|توضیح|
|---|---|
|عملیات باید روی نامه‌ای معتبر انجام شده باشد|بررسی وجود `LetterId` الزامی است|
|عملیات باید شناخته‌شده باشد|بررسی معتبر بودن `ActionType`|

---

### 📥 ورودی‌ها (Input)

|فیلد|نوع|الزامی؟|توضیح|
|---|---|---|---|
|`LetterId`|`Guid`|✅|نامه‌ای که عملیات روی آن انجام شده|
|`ActionType`|`enum`|✅|نوع عمل انجام‌شده (Create, Edit, Delete, Restore, Forward, etc.)|
|`PerformedByUserId`|`Guid`|✅|کاربری که عملیات را انجام داده|
|`PerformedAt`|`DateTime`|❌|اگر داده نشود، زمان فعلی ثبت می‌شود|
|`Metadata`|`string?`|❌|توضیحات اضافی یا داده‌های خاص عملیات|
|`IpAddress`|`string?`|❌|در صورت نیاز به ثبت IP|

---

### ⚙️ مراحل اجرایی

1. اعتبارسنجی ورودی‌ها
    
2. ساخت یک رکورد `LetterLog`
    
3. ذخیره در دیتابیس
    
4. بازگشت موفقیت یا خطا
    

---

### 📤 خروجی (Output)

|فیلد|نوع|توضیح|
|---|---|---|
|`Success`|`bool`|نتیجه موفقیت‌آمیز بودن عملیات|
|`Message`|`string`|پیام خروجی|
|`LoggedActionId`|`Guid`|شناسه لاگ ثبت‌شده|

---

### 🧱 مدل `LetterLog`

|فیلد|نوع|توضیح|
|---|---|---|
|`Id`|`Guid`|شناسه لاگ|
|`LetterId`|`Guid`|نامه مرتبط|
|`ActionType`|`enum`|نوع عملیات (از پیش تعریف‌شده)|
|`PerformedByUserId`|`Guid`|کاربر اجراکننده|
|`PerformedAt`|`DateTime`|زمان اجرا|
|`Metadata`|`string?`|اطلاعات اضافه|
|`IpAddress`|`string?`|IP کاربر (در صورت وجود)|

---

### 📘 Enum پیشنهادی برای `ActionType`:

enum LetterActionType {
  Created,
  Edited,
  Deleted,
  Restored,
  Sent,
  Forwarded,
  Replied,
  Viewed,
  Archived,
  Unarchived,
  Commented,
  PermissionAssigned,
  PermissionRevoked,
  TagAdded,
  TagRemoved,
  AttachmentAdded,
  AttachmentRemoved
}


### 🔒 نکات امنیتی:

- این Use Case توسط سیستم و درون سایر Use Caseها فراخوانی می‌شود.
    
- کاربر مستقیم آن را اجرا نمی‌کند، بلکه در انتهای هر عملیات روی نامه‌ها ثبت می‌شود.