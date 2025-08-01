

### پیگیری تاریخچه مشاهده و دسترسی به یک نامه

---

### 🎯 هدف:

امکان مشاهده‌ی لیست کاربرانی که یک نامه را باز کرده‌اند یا به آن دسترسی داشته‌اند، به‌همراه تاریخ و جزئیات دسترسی.

---

### ✅ سناریوهای کاربردی

|سناریو|توضیح|
|---|---|
|بررسی اینکه چه کسی نامه را خوانده است|در نامه‌های مهم یا ارجاعی|
|نظارت امنیتی یا مدیریتی|بررسی سطح دسترسی کاربران و کنترل نشت اطلاعات|
|ثبت سوابق برای تحلیل رفتار کاربران|در اتوماسیون‌های حساس یا دولتی|

---

### 📥 ورودی‌ها (Input)

|فیلد|نوع|الزامی؟|توضیح|
|---|---|---|---|
|`LetterId`|`Guid`|✅|شناسه نامه موردنظر|
|`RequesterUserId`|`Guid`|✅|کاربر درخواست‌کننده اطلاعات|
|`FromDate`|`DateTime?`|❌|فیلتر تاریخ شروع (اختیاری)|
|`ToDate`|`DateTime?`|❌|فیلتر تاریخ پایان (اختیاری)|

---

### ⚙️ مراحل اجرا

1. **بررسی سطح دسترسی کاربر درخواست‌کننده**
    
    - فقط کاربران مجاز (مثلاً مدیر، مالک نامه یا امنیت سیستم) امکان مشاهده این اطلاعات را دارند.
        
2. **جستجو در موجودیت `LetterViewHistory`**
    
    - استخراج رکوردهای `LetterId = X` با تاریخ بین `FromDate` تا `ToDate` (در صورت وجود)
        
3. **مرتب‌سازی و بازگردانی اطلاعات**
    

---

### 📤 خروجی (Output)

|فیلد|نوع|توضیح|
|---|---|---|
|`UserId`|`Guid`|شناسه کاربر بیننده|
|`UserName`|`string`|نام کامل کاربر|
|`AccessDate`|`DateTime`|زمان مشاهده نامه|
|`AccessType`|`enum`|نوع دسترسی: مشاهده، چاپ، دانلود PDF، ارجاع و...|

---

### 📎 نکات مهم

- این اطلاعات از موجودیت `LetterViewHistory` تأمین می‌شود که باید به‌صورت **خودکار** در هنگام مشاهده یا اقدام روی نامه پر شود.
    
- برای هر مشاهده جدید، در صورت فاصله زمانی زیاد (مثلاً بیشتر از ۵ دقیقه یا اولین بار)، یک رکورد جدید ثبت می‌شود.
    
- این قابلیت یکی از ارکان **ممیزی امنیتی سیستم** است.
    
- می‌توان فیلترهای جستجو مثل کاربر خاص، نوع دسترسی یا بازه زمانی هم اضافه کرد.