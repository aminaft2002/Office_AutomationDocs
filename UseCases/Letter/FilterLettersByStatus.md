
### فیلتر کردن نامه‌ها بر اساس وضعیت (Status)

---

### 🎯 هدف:

امکان مشاهده لیست نامه‌ها با وضعیت خاص مانند «پیش‌نویس»، «ارسال‌شده»، «ارجاع‌شده»، «بایگانی‌شده» و ... با درنظر گرفتن سطح دسترسی کاربر.

---

### ✅ سناریوهای کاربردی

|سناریو|توضیح|
|---|---|
|نمایش همه پیش‌نویس‌های من|کاربر پیش‌نویس‌های خود را مشاهده می‌کند|
|مشاهده نامه‌های خوانده‌نشده|فیلتر بر اساس `Status = Unread` (در LetterViewHistory)|
|مرور نامه‌های بایگانی‌شده واحد خاص|`Status = Archived` و `SenderUnitId` خاص|
|پیگیری نامه‌های در حال ارجاع یا پاسخ|فیلترهای ترکیبی با `Status = Referred` یا `Status = Responded`|

---

### 📥 ورودی‌ها (Input)

|فیلد|نوع|الزامی؟|توضیح|
|---|---|---|---|
|`Status`|`LetterStatus`|✅|وضعیت موردنظر|
|`UserId`|`Guid`|✅|کاربر جستجوکننده (برای بررسی سطح دسترسی)|
|`SenderUnitId`|`Guid?`|❌|فیلتر واحد فرستنده|
|`ReceiverUnitId`|`Guid?`|❌|فیلتر واحد گیرنده|
|`Priority`|`LetterPriority?`|❌|فیلتر اولویت|
|`Confidentiality`|`LetterConfidentiality?`|❌|محرمانگی|
|`DateFrom`|`DateTime?`|❌|تاریخ شروع|
|`DateTo`|`DateTime?`|❌|تاریخ پایان|
|`PageIndex`|`int`|✅|شماره صفحه|
|`PageSize`|`int`|✅|اندازه صفحه|

---

### ⚙️ مراحل اجرا

1. بررسی دسترسی کاربر به نامه‌ها
    
2. فیلتر بر اساس `Status`
    
3. اعمال فیلترهای دیگر (تاریخ، اولویت، محرمانگی و...)
    
4. مرتب‌سازی و صفحه‌بندی
    
5. بازگرداندن خروجی به‌صورت امن و بهینه
    

---

### 📤 خروجی (Output)

|فیلد|نوع|توضیح|
|---|---|---|
|`TotalCount`|`int`|تعداد کل نتایج|
|`Letters`|`List<LetterSummaryDto>`|لیست خلاصه نامه‌ها|
|`PageIndex`|`int`|صفحه فعلی|
|`PageSize`|`int`|اندازه صفحه|

---

### 📄 مدل `LetterSummaryDto`

همان مدل استاندارد برای نمایش خلاصه نامه شامل:

- `Id`
    
- `Subject`
    
- `LetterNumber`
    
- `SenderName`
    
- `RegisterDate`
    
- `Status`
    
- `Priority`
    
- `IsConfidential`
    

---

### 🔐 نکات امنیتی

- نامه‌های محرمانه فقط در صورت داشتن دسترسی نمایش داده می‌شوند.
    
- برای پیش‌نویس‌ها، فقط کاربر ایجادکننده قادر به مشاهده است مگر دسترسی خاصی داشته باشد.