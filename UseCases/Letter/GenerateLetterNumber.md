

### 📄 Use Case: GenerateLetterNumber

|ویژگی|مقدار|
|---|---|
|**نام یوزکیس**|GenerateLetterNumber|
|**هدف**|تولید یک شماره یکتا برای نامه بر اساس الگوی تعیین‌شده، جهت درج در فیلد `LetterNumber`|
|**Actor**|سیستم (اتوماتیک) یا کاربر در هنگام نهایی‌سازی یا ارسال نامه|
|**Trigger**|ارسال نامه یا ثبت نهایی پیش‌نویس در سیستم توسط کاربر یا فرآیند بک‌اند|

---

### 🧩 Preconditions (پیش‌نیازها):

- نامه در وضعیت `Draft` یا بدون شماره باشد.
    
- الگوی شماره‌گذاری (Template/Pattern) از پیش تعیین شده باشد (مثلاً: `YYYY-MM-UnitCode-Sequence`).
    

---

### ⚙️ Main Flow (روند اصلی):

1. سیستم بررسی می‌کند که آیا نامه در وضعیت مجاز برای شماره‌گذاری است یا خیر.
    
2. الگوی شماره‌گذاری از تنظیمات سیستم یا واحد سازمانی استخراج می‌شود.
    
3. اجزای الگو مانند `تاریخ، کد واحد، شمارنده` با مقادیر جاری جایگزین می‌شوند.
    
4. یک شماره یکتا بر اساس این الگو تولید می‌شود:
    
    - بررسی می‌شود که این شماره در دیتابیس تکراری نباشد.
        
    - در صورت تکرار، شمارنده افزایش یافته و مجدد امتحان می‌شود.
        
5. شماره نهایی در فیلد `LetterNumber` ذخیره می‌شود.
    
6. وضعیت نامه در صورت نیاز از `Draft` به `Registered` یا `Sent` تغییر می‌یابد.
    
7. نتیجه به کاربر یا ماژول فراخوان بازگردانده می‌شود.
    

---

### 🔄 Alternative Flow (جایگزین):

|شماره|شرط|نتیجه|
|---|---|---|
|A1|الگوی شماره‌گذاری تعریف نشده|خطای `ConfigurationMissingException` بازگردانده شود|
|A2|شمارنده به حداکثر مقدار مجاز رسید|خطای `SequenceOverflowException` صادر شود|
|A3|نامه قبلاً شماره‌گذاری شده است|عملیات متوقف شده و پیام `LetterAlreadyNumbered` بازگردانده شود|

---

### 📦 Output (خروجی):

{
  "letterId": "uuid",
  "letterNumber": "1403-05-HR-0247",
  "status": "Success"
}
### ⚙️ گزینه‌های قابل تنظیم:

|گزینه|توضیح|
|---|---|
|`Pattern`|الگوی شماره‌گذاری، مثلاً: `{yyyy}/{mm}/DEP-{sequence:4}`|
|`UnitScoped`|آیا شمارنده مختص هر واحد سازمانی باشد؟|
|`DailyReset`|آیا شمارنده در هر روز ریست شود؟|
|`PreviewMode`|فقط پیش‌نمایش شماره تولیدی، بدون ذخیره نهایی|

---

### 🛡️ نکات امنیتی:

- فقط کاربران مجاز به ارسال یا نهایی‌سازی نامه می‌توانند شماره‌گذاری انجام دهند.
    
- سیستم باید از تکراری نبودن شماره‌ها به‌طور دقیق جلوگیری کند (Transaction Safe).
    

---

### 📚 وابستگی‌ها:

- Entity: `Letter`
    
- Table: `LetterNumberSequence` (برای پیگیری شمارنده‌ها)
    
- Setting: `LetterNumberingPattern`, `ResetPolicy`, `ScopedByUnit`

