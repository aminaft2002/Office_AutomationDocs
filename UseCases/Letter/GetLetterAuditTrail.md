
### 📄 Use Case: GetLetterAuditTrail

|ویژگی|مقدار|
|---|---|
|**نام یوزکیس**|GetLetterAuditTrail|
|**هدف**|نمایش کامل تاریخچه تمامی اقدامات (Logs) انجام‌شده روی یک نامه مشخص توسط کاربران مختلف|
|**Actor**|کاربر مجاز به مشاهده تاریخچه نامه|
|**Trigger**|کاربر روی دکمه "تاریخچه اقدامات" یا "Audit Trail" در صفحه جزئیات نامه کلیک می‌کند|

---

### 🧩 Preconditions (پیش‌نیازها):

- نامه باید در سیستم موجود باشد.
    
- کاربر باید دارای دسترسی مشاهده آن نامه باشد.
    

---

### ⚙️ Main Flow (روند اصلی):

1. کاربر درخواست مشاهده تاریخچه اقدامات یک نامه خاص را ارسال می‌کند.
    
2. سیستم `LetterId` را دریافت کرده و صحت آن را بررسی می‌کند.
    
3. سیستم تمامی رکوردهای موجود در جدول `LetterLog` مربوط به آن نامه را بازیابی می‌کند.
    
4. هر رکورد شامل اطلاعاتی مثل نوع عملیات، کاربر انجام‌دهنده، زمان و توضیح است.
    
5. سیستم لیست را به ترتیب زمانی (جدیدترین به قدیمی‌ترین) نمایش می‌دهد.
    

---

### 🔄 Alternative Flow (روند جایگزین):

|شماره|شرط|روند جایگزین|
|---|---|---|
|A1|نامه‌ای با این شناسه وجود ندارد|نمایش خطای 404 - Letter Not Found|
|A2|کاربر مجاز به مشاهده نامه نیست|نمایش خطای 403 - Access Denied|

---

### 📦 Output (خروجی):

[
  {
    "logId": "guid",
    "letterId": "guid",
    "actionType": "enum (Created, Updated, Sent, Archived, Restored, Deleted, Viewed, etc)",
    "performedBy": {
      "userId": "guid",
      "fullName": "string"
    },
    "performedAt": "datetime",
    "description": "string"
  },
  ...
]
### 📚 وابستگی‌ها:

- Entity: `LetterLog`
    
- Relation: `Letter 1:N LetterLog`