### 📄 Use Case: UpdateLetterStatus

|ویژگی|مقدار|
|---|---|
|**نام یوزکیس**|UpdateLetterStatus|
|**هدف**|تغییر وضعیت (Status) نامه به یکی از حالت‌های مجاز بر اساس عملیات انجام‌شده|
|**Actor**|کاربر مجاز (مثلاً مسئول ثبت، گیرنده، مدیر واحد)، یا سیستم|
|**Trigger**|عملیات‌هایی مانند ارسال، ارجاع، پاسخ، بستن یا خوانده‌شدن نامه رخ می‌دهند|

---

### 🧩 Preconditions (پیش‌نیازها):

- کاربر باید دسترسی و مجوز لازم برای انجام عملیات داشته باشد.
    
- نامه موردنظر باید وجود داشته باشد.
    
- وضعیت فعلی نامه باید اجازه‌ی انتقال به وضعیت جدید را بدهد (مثلاً نامه بسته‌شده نباشد).
    

---

### 📊 وضعیت‌های ممکن (LetterStatus Enum):
enum LetterStatus {
  Draft,
  Registered,
  Sent,
  Received,
  Read,
  Referred,
  Responded,
  Archived,
  Closed
}

### 🔄 Transitions مجاز:

|وضعیت فعلی|وضعیت مجاز بعدی|
|---|---|
|Draft|Registered, Sent|
|Registered|Sent|
|Sent|Received, Referred, Read|
|Received|Read, Referred|
|Referred|Responded|
|Responded|Closed|
|Any|Archived|
|Archived|Unarchived|

---

### ⚙️ Main Flow (روند اصلی):

1. کاربر یا سیستم، درخواست تغییر وضعیت را با `LetterId` و `NewStatus` ارسال می‌کند.
    
2. سیستم بررسی می‌کند که این تغییر وضعیت مجاز است.
    
3. در صورت مجاز بودن:
    
    - وضعیت جدید در دیتابیس ثبت می‌شود.
        
    - رکوردی در `LetterLog` اضافه می‌شود.
        
    - در صورت نیاز، نوتیفیکیشن ارسال می‌گردد.
        
4. در صورت نامعتبر بودن وضعیت:
    
    - عملیات رد شده و پیام خطا باز می‌گردد.
        

---

### 🔄 Alternative Flow (استثنائات):

|شماره|شرط|نتیجه|
|---|---|---|
|A1|وضعیت مقصد غیرمجاز است|پیام: `InvalidStatusTransitionException`|
|A2|کاربر مجوز ندارد|پیام: `PermissionDeniedException`|
|A3|نامه وجود ندارد|پیام: `LetterNotFoundException`|
|A4|نامه در وضعیت نهایی است (Closed)|پیام: `CannotUpdateClosedLetterException`|

---

### 📦 Output (نمونه خروجی موفق):

{
  "success": true,
  "newStatus": "Referred",
  "timestamp": "2025-07-28T14:52:00Z"
}


### 🔐 نکات امنیتی:

- اعتبارسنجی نقش کاربر انجام می‌شود (مثلاً فقط فرستنده می‌تواند `Sent` کند).
    
- ثبت لاگ برای هر تغییر وضعیت اجباری است (`LetterLog`).
    

---

### 📚 وابستگی‌ها:

- Entity: `Letter`, `LetterLog`
    
- Enum: `LetterStatus`
    
- Table: `LetterPermissions`
    
- یوزکیس‌های مرتبط: `SendLetter`, `ReceiveLetter`, `ArchiveLetter`, `MarkLetterAsRead`
- 