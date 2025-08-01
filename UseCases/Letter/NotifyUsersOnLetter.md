

### 🎯 هدف:

اطلاع‌رسانی خودکار به کاربران مرتبط با یک نامه، هنگام وقوع رویدادهایی مانند: ارجاع، پاسخ، ویرایش، ارسال، یا هر رویداد مهم دیگر.

---

### ✅ موارد استفاده (Use Scenarios)

|سناریو|توضیح|
|---|---|
|نامه‌ای ارجاع داده می‌شود|گیرنده جدید باید اعلان دریافت کند|
|پاسخی به نامه داده می‌شود|فرستنده یا واحد اولیه باید مطلع شود|
|نامه‌ای ویرایش می‌شود|در صورت تغییر وضعیت، گیرنده جدید یا مسئول پیگیری باید اعلان دریافت کند|
|نامه‌ای برای شما ارسال شده|کاربران مرتبط باید هشدار بگیرند|

---

### 📥 ورودی‌ها (Input)

|فیلد|نوع|الزامی؟|توضیح|
|---|---|---|---|
|`LetterId`|`Guid`|✅|نامه‌ای که برای آن اعلان ارسال می‌شود|
|`TriggeredByUserId`|`Guid`|✅|کاربری که باعث رویداد شده|
|`NotificationType`|`enum`|✅|نوع اعلان (ارجاع، پاسخ، ارسال...)|
|`TargetUserIds`|`List<Guid>`|✅|لیست کاربرانی که باید اعلان دریافت کنند|
|`Message`|`string`|✅|محتوای اعلان یا توضیح|
|`Url`|`string?`|❌|لینک مستقیم به نامه در UI برای هدایت سریع|
|`CreatedAt`|`DateTime`|❌|در صورت عدم ارسال، زمان فعلی در نظر گرفته می‌شود|

---

### ⚙️ مراحل اجرایی

1. اعتبارسنجی ورودی‌ها و `LetterId`
    
2. ساخت چند رکورد `LetterNotification` برای هر کاربر
    
3. ثبت رکوردها در دیتابیس
    
4. انتشار اعلان‌ها به سیستم اعلان (مثلاً WebSocket یا Email یا Push Notification)
    

---

### 📤 خروجی (Output)

|فیلد|نوع|توضیح|
|---|---|---|
|`Success`|`bool`|نتیجه عملیات|
|`NotificationIds`|`List<Guid>`|لیست شناسه اعلان‌های ثبت‌شده|
|`Message`|`string`|پیام خروجی موفقیت یا خطا|

---

### 📦 مدل `LetterNotification`

|فیلد|نوع|توضیح|
|---|---|---|
|`Id`|`Guid`|شناسه یکتا|
|`LetterId`|`Guid`|نامه مربوطه|
|`UserId`|`Guid`|کاربری که باید اعلان بگیرد|
|`NotificationType`|`enum`|نوع اعلان|
|`Message`|`string`|پیام قابل نمایش|
|`Url`|`string?`|لینک مستقیم به نامه|
|`IsRead`|`bool`|وضعیت خوانده شدن|
|`CreatedAt`|`DateTime`|زمان ثبت اعلان|

---

### 🔘 Enum: `NotificationType`

csharp



enum LetterNotificationType {
  Sent,
  Forwarded,
  Replied,
  Referred,
  Commented,
  Edited,
  Archived,
  PermissionAssigned,
  TagAdded
}


---

### 🔒 نکات مهم:

- باید از تکرار اعلان برای یک کاربر جلوگیری شود (مثلاً اگر نامه‌ای چند بار ارجاع شود در زمان کوتاه، فقط یک اعلان ثبت شود).
    
- سیستم باید قابلیت غیرفعال‌سازی اعلان‌ها یا تغییر نوع آن‌ها برای هر کاربر را در آینده داشته باشد (اختیاری).