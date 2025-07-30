
### 📄 Use Case: ValidateLetterBeforeSend

|ویژگی|مقدار|
|---|---|
|**نام یوزکیس**|ValidateLetterBeforeSend|
|**هدف**|بررسی صحت و کامل بودن اطلاعات نامه قبل از ارسال رسمی|
|**Actor**|کاربر ارسال‌کننده، سیستم (قبل از عملیات Send)|
|**Trigger**|کاربر دکمه "ارسال نامه" را می‌زند یا API مربوطه فراخوانی می‌شود|

---

### 🧩 Preconditions (پیش‌نیازها):

- نامه در وضعیت `Draft` یا `Registered` باشد.
    
- کاربر دسترسی کافی برای ارسال نامه را داشته باشد.
    
- فیلدهای ضروری باید پر شده باشند.
    

---

### ✅ Validation Rules (قوانین اعتبارسنجی):

|شرط|توضیح|
|---|---|
|`Subject` نباید خالی باشد|عنوان نامه اجباری است|
|`Body` باید حداقل یک پاراگراف داشته باشد|محتوای نامه باید مشخص باشد|
|`SenderUnitId` و `CreatorUserId` باید مقدار داشته باشند|فرستنده مشخص باشد|
|`LetterType` مقدار معتبر باشد|نوع نامه مشخص شود|
|اگر `LetterType == Outgoing` یا `Incoming`|باید حداقل یک گیرنده مشخص باشد|
|اگر `IsConfidential == true`|باید دسترسی خاص تنظیم شده باشد (`LetterPermissions`)|
|اگر `LetterTemplateId` تنظیم شده باشد|ساختار متن باید با الگو تطابق داشته باشد (اختیاری)|
|پیوست‌ها اگر اجباری باشند (بنا بر تنظیمات سیستم)|حداقل یک `Attachment` باید ثبت شده باشد|
|اگر نامه پاسخ به نامه‌ای دیگر است (`ResponseToLetterId`)|نامه مرجع باید وجود داشته باشد و بسته نشده باشد|

---

### ⚙️ Main Flow (روند اصلی):

1. سیستم نامه مورد نظر را بارگذاری می‌کند.
    
2. قواعد اعتبارسنجی بالا به‌ترتیب بررسی می‌شوند.
    
3. در صورت عبور از تمام شروط، پاسخ `Valid` بازگردانده می‌شود.
    
4. در غیر این صورت، پیام خطا شامل لیست اشکالات بازگردانده می‌شود.
    

---

### 🔄 Alternative Flow (جایگزین‌ها):

|شماره|شرط|نتیجه|
|---|---|---|
|A1|`Subject` خالی است|پیام خطای: `SubjectIsRequired`|
|A2|گیرنده مشخص نیست|پیام: `ReceiverMissing`|
|A3|دسترسی‌های نامه تنظیم نشده|پیام: `LetterPermissionRequired`|
|A4|قالب نامه با الگو تطابق ندارد|پیام: `TemplateMismatchException`|
|A5|نامه قبلاً ارسال شده|پیام: `LetterAlreadySent` و توقف عملیات|

---

### 📦 Output (خروجی نمونه):

{
  "isValid": false,
  "errors": [
    "Subject is required",
    "Receiver is missing",
    "Confidential letter must have explicit permissions"
  ]
}


### 🔐 نکات امنیتی:

- بررسی می‌شود که کاربر مجوز بررسی یا ارسال این نامه را داشته باشد.
    
- نتیجه اعتبارسنجی نباید اطلاعات محرمانه به کاربر غیرمجاز ارائه دهد.
    

---

### 📚 وابستگی‌ها:

- Entity: `Letter`
    
- Table: `LetterPermissions`, `LetterRecipients`
    
- Setting: `LetterTemplate`, `LetterConfidentialityPolicy`