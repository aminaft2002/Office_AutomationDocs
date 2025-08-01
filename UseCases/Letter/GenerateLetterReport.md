

### 📄 Use Case: GenerateLetterReport

|ویژگی|مقدار|
|---|---|
|**نام یوزکیس**|GenerateLetterReport|
|**هدف**|تولید یک گزارش تحلیلی یا آماری از مجموعه‌ای از نامه‌ها بر اساس فیلترها و معیارهای تعریف‌شده|
|**Actor**|مدیر سیستم، مسئول دبیرخانه، کاربر مجاز|
|**Trigger**|کاربر از صفحه گزارشات اقدام به تولید گزارش با فیلترهای خاص می‌کند|

---

### 🧩 Preconditions (پیش‌نیازها):

- کاربر باید دسترسی به بخش گزارشات داشته باشد.
    
- فیلترهای معتبر و ساختارمند ارسال شده باشند (مثلاً تاریخ، وضعیت، نوع نامه، واحد فرستنده، گیرنده و...).
    

---

### ⚙️ Main Flow (روند اصلی):

1. کاربر درخواست تولید گزارش را با فیلترهای زیر ارسال می‌کند:
    
    - بازه تاریخی ثبت یا تاریخ نامه
        
    - نوع نامه (وارده، صادره، داخلی)
        
    - وضعیت نامه (پیش‌نویس، خوانده‌شده، آرشیوشده و...)
        
    - واحدهای فرستنده/گیرنده
        
    - برچسب‌ها
        
    - کاربر ایجادکننده یا ارسال‌کننده
        
2. سیستم داده‌ها را از پایگاه داده واکشی می‌کند.
    
3. اطلاعات به‌صورت یک گزارش آماری یا جدولی ساختار یافته در فرمت‌های زیر تولید می‌شود:
    
    - گزارش جدول HTML
        
    - فایل Excel (xlsx)
        
    - فایل PDF
        
4. نتیجه نهایی به کاربر نمایش داده شده یا برای دانلود آماده می‌شود.
    

---

### 🧾 فیلدهای رایج در گزارش خروجی:

|فیلد|توضیح|
|---|---|
|LetterNumber|شماره نامه|
|Subject|موضوع|
|SenderName / Org|فرستنده|
|ReceiverName / Org|گیرنده|
|Status|وضعیت نامه|
|LetterDate|تاریخ نامه|
|RegistrationDate|تاریخ ثبت|
|Type|نوع نامه|
|Confidentiality|محرمانگی|
|Tags|برچسب‌ها|

---

### 🔄 Alternative Flows (استثنائات):

|شماره|شرط|نتیجه|
|---|---|---|
|A1|هیچ نامه‌ای با فیلترهای اعمال‌شده یافت نشد|پیام: "گزارشی برای شرایط انتخاب‌شده موجود نیست"|
|A2|فرمت گزارش نامعتبر است|پیام: "UnsupportedReportFormatException"|
|A3|کاربر مجوز لازم برای مشاهده داده‌ها ندارد|پیام: "PermissionDeniedException"|

---

### 🖨️ خروجی نهایی:

- فایل PDF یا Excel یا نمای HTML
    
- قابل فیلتر، دسته‌بندی و صفحه‌بندی
    

---

### 🔐 نکات امنیتی:

- فقط اطلاعات در محدوده دسترسی کاربر نمایش داده می‌شود.
    
- اطلاعات محرمانه فقط در صورت مجوز قابل نمایش هستند.
    

---

### 📚 وابستگی‌ها:

- Entity: `Letter`, `LetterTag`, `LetterPermission`
    
- UseCases: `SearchLetters`, `FilterLettersByStatus`, `ExportLetterAsPdf`