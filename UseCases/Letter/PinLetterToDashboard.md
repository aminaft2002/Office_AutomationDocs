
### پین‌کردن یک نامه روی داشبورد کاربر برای دسترسی سریع

---

### 🎯 هدف:

کاربر بتواند نامه‌ای را که برایش مهم یا پرتکرار است، روی داشبورد خود پین کند تا سریع‌تر به آن دسترسی داشته باشد.

---

### ✅ سناریوهای کاربردی

|سناریو|توضیح|
|---|---|
|کاربر بخواهد یک نامه خاص را همیشه جلوی چشم داشته باشد|مثل نامه‌های ارجاعی یا بحرانی|
|لیست نامه‌های پین‌شده در داشبورد نمایش داده می‌شود|مستقل از فیلترهای دیگر|
|در برخی سیستم‌ها، حداکثر تعداد پین مشخص می‌شود|مثلاً حداکثر ۵ نامه قابل پین شدن|

---

### 📥 ورودی‌ها (Input)

|فیلد|نوع|الزامی؟|توضیح|
|---|---|---|---|
|`LetterId`|`Guid`|✅|شناسه نامه مورد نظر|
|`UserId`|`Guid`|✅|شناسه کاربر در حال پین کردن|

---

### ⚙️ مراحل اجرا

1. بررسی وجود نامه و سطح دسترسی کاربر به آن
    
2. بررسی اینکه قبلاً همین نامه توسط کاربر پین نشده باشد
    
3. ذخیره یک رکورد جدید در موجودیت `PinnedLetter` (با `UserId` و `LetterId`)
    
4. بازگرداندن نتیجه موفقیت یا خطا
    

---

### 📤 خروجی (Output)

|فیلد|نوع|توضیح|
|---|---|---|
|`Success`|`bool`|نتیجه عملیات|
|`Message`|`string`|پیام موفقیت یا خطا|

---

### 🗃 موجودیت مربوطه

csharp

CopyEdit

`PinnedLetter {   Id: Guid   UserId: Guid   LetterId: Guid   PinnedAt: DateTime }`

---

### 📎 نکات طراحی

- در داشبورد کاربر، لیست `PinnedLetters` باید با زمان `PinnedAt` مرتب شده باشد.
    
- اگر نیاز به ترتیب دستی باشد، فیلدی مثل `Order` هم قابل اضافه شدن است.
    
- قابلیت UnpinLetter نیز باید طراحی شود تا کاربر بتواند پین را بردارد.