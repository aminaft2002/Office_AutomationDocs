

|فیلد|نوع داده|توضیحات|
|---|---|---|
|`Id`|GUID|شناسه یکتا|
|`Title`|string|عنوان سند|
|`Description`|string (nullable)|توضیح اختیاری درباره سند|
|`FileName`|string|نام فایل ذخیره‌شده در سرور|
|`OriginalFileName`|string|نام اصلی فایل که کاربر آپلود کرده|
|`FileSize`|int|حجم فایل بر حسب بایت|
|`MimeType`|string|نوع فایل (PDF, JPEG, Word, ...)|
|`UploadDate`|datetime|تاریخ آپلود فایل|
|`UploaderUserId`|GUID|کاربری که فایل را بارگذاری کرده|
|`CategoryId`|GUID (nullable)|دسته‌بندی سند|
|`Tags`|list|برچسب‌ها برای جستجوپذیری بهتر|
|`IsArchived`|bool|آیا سند بایگانی شده است؟|
|`LinkedLetterId`|GUID (nullable)|اگر این فایل به نامه‌ای وابسته است|


### 📌 توضیحات طراحی:

- `OriginalFileName` برای نمایش به کاربر در رابط کاربری
    
- `MimeType` به سیستم اجازه می‌دهد نوع فایل را مدیریت کند
    
- `LinkedLetterId` باعث می‌شود در صورت نیاز، یک فایل هم به نامه لینک شود و هم در بایگانی عمومی باشد
    
- `Tags` برای آینده‌نگری در جستجوی هوشمند طراحی شده