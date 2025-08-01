
|نام فیلد|نوع داده|الزامی؟|توضیحات|
|---|---|---|---|
|`id`|Integer (PK)|✅|شناسه یکتا|
|`title`|String|✅|عنوان قالب|
|`content`|Text / HTML|✅|متن کامل قالب با متغیرهای پویا (مثال: `{{ReceiverName}}`)|
|`description`|String|❌|توضیح کاربرد یا نکات قالب|
|`category`|String / Enum|❌|دسته‌بندی قالب (حقوقی، عمومی، منابع انسانی...)|
|`isActive`|Boolean|❌|فعال بودن قالب|
|`createdBy`|FK (User)|✅|کاربری که قالب را ایجاد کرده|
|`createdAt`|DateTime|✅|زمان ایجاد|
|`updatedAt`|DateTime|✅|زمان به‌روزرسانی|

## 🧠 ساختار متغیرهای پویا

برای ساختار متغیرها از **`{{VariableName}}`** استفاده می‌کنیم که توسط سیستم در زمان ساخت نامه، با مقدار واقعی جایگزین می‌شود.

|Placeholder|توضیح|
|---|---|
|`{{ReceiverName}}`|نام گیرنده نامه|
|`{{SenderName}}`|نام فرستنده|
|`{{CurrentDate}}`|تاریخ ایجاد نامه|
|`{{LetterNumber}}`|شماره نامه|
|`{{Subject}}`|موضوع نامه|
|`{{AttachmentCount}}`|تعداد پیوست‌ها|


### 🧩 پشتیبانی از متغیرهای پویا

در فیلد `Body` از متغیرهایی مانند:

- `{{SenderName}}`
    
- `{{ReceiverName}}`
    
- `{{CurrentDate}}`
    

استفاده می‌شود که هنگام نهایی‌سازی نامه جایگزین می‌گردند.

---

### 🔁 روابط

- `LetterTemplate → User` (Many-to-One)
    
- `Letter → LetterTemplate` (Many-to-One): هر نامه می‌تواند از یک الگو ساخته شود
