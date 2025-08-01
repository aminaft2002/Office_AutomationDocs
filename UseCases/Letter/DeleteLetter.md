با در نظر گرفتن منطق کسب‌وکار در اتوماسیون اداری، حذف کامل نامه معمولاً مجاز نیست مگر در وضعیت **پیش‌نویس**. نامه‌های ارسال‌شده باید **غیرقابل حذف** باشند (به‌دلایل حقوقی و سیستمی).

---

## 🧾 Use Case: DeleteLetter

|ویژگی|مقدار|
|---|---|
|**شناسه**|`UC_DeleteLetter`|
|**هدف**|حذف کامل یک نامه پیش‌نویس توسط سازنده|
|**بازیگران اصلی**|`CreatorUser`|
|**پیش‌شرط‌ها**|- نامه در وضعیت `Draft` باشد  <br>- کاربر همان `CreatorUser` نامه باشد|
|**محرک**|کاربر روی دکمه "حذف" کلیک می‌کند|
|**جریان اصلی**|1. سیستم بررسی می‌کند که نامه در وضعیت Draft است  <br>2. بررسی می‌شود کاربر سازنده نامه است  <br>3. تمام پیوست‌ها، یادداشت‌ها و دسترسی‌های مرتبط نیز حذف می‌شوند  <br>4. رکورد از دیتابیس حذف می‌شود (Soft Delete یا Hard Delete بسته به سیاست سیستم)|
|**جریان جایگزین‌ها**|- اگر نامه Finalized یا ارسال‌شده باشد، پیام خطا نشان داده می‌شود: `امکان حذف نامه پس از ارسال وجود ندارد.`  <br>- اگر کاربر غیرمجاز باشد، پیام: `شما اجازه حذف این نامه را ندارید.`|
|**نتیجه نهایی**|نامه و وابستگی‌هایش از سیستم حذف می‌شوند|
|**پس‌شرط‌ها**|- رکورد در صورت Hard Delete از DB پاک شده  <br>- یا در صورت Soft Delete، فیلد `IsDeleted = true` تنظیم می‌شود|
|**ملاحظات امنیتی**|حذف فقط توسط صاحب اصلی و در وضعیت Draft|

---

## 🔐 قانون دسترسی (Permission)

|نقش|اجازه حذف|
|---|---|
|`Creator`|✅ فقط در حالت Draft|
|`Admin`|🔒 فقط از طریق مسیر مدیریتی خاص (Audit یا Recovery)|
|`OtherUser`|❌ ندارد|

---

آیا بخوایم برای `Soft Delete` پیاده‌سازی کنیم که بعداً بازیابی بشه، یا حذف واقعی باشه (`Hard Delete`)؟

بعدش آماده‌ام بریم سراغ Use Case بعدی. بگو کدوم رو کار کنیم؟

##### You said:

Soft Delete

###### ChatGPT said:

عالی! پس برای Use Case ‌`DeleteLetter` از **الگوی Soft Delete** استفاده می‌کنیم. در این مدل، رکورد از دیتابیس پاک نمی‌شه، بلکه فقط علامت‌گذاری می‌شه که دیگه در فهرست‌ها و جست‌وجوها نمایش داده نشه. این کار به بازیابی، گزارش‌گیری و ردگیری فعالیت‌ها کمک می‌کنه.

---

## 🔁 بروزرسانی Use Case: DeleteLetter (با Soft Delete)

|ویژگی|مقدار|
|---|---|
|**نوع حذف**|`Soft Delete`|
|**فیلد کنترلی**|`IsDeleted: bool = true`  <br>`DeletedAt: DateTime?`  <br>`DeletedBy: Guid?`|
|**تأثیر در سایر بخش‌ها**|- در همه کوئری‌ها `WHERE IsDeleted = false` لحاظ می‌شود  <br>- در پنل ادمین می‌توان نامه‌های حذف‌شده را مشاهده و بازیابی کرد|
|**مزایا**|قابل بازیابی، مناسب برای بررسی امنیتی، لاگ بهتر|
|**پیشنهاد امنیتی**|دسترسی بازیابی فقط برای Adminها|

---

## 📦 تغییرات در مدل Letter:

csharp

CopyEdit

`public class Letter {     public bool IsDeleted { get; set; } = false;     public DateTime? DeletedAt { get; set; }     public Guid? DeletedBy { get; set; } }`

---

## 📌 نکات پیاده‌سازی

1. در همه Repositoryها و Queryها باید شرط `!IsDeleted` اضافه شود.
    
2. UI نمایش حذف به صورت "آیا مطمئنید؟" و سپس مخفی‌سازی در لیست.
    
3. پنل مدیریت برای بازیابی یا مشاهده تاریخچه حذف در آینده طراحی خواهد شد.