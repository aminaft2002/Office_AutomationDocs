
### 🎯 هدف

نهایی‌سازی نامه و ثبت رسمی آن به‌عنوان یک نامه ارسال‌شده یا داخلی.

---

### 🧑‍💻 بازیگران (Actors)

- کاربر ایجادکننده نامه (CreatorUser)
    

---

### 🛑 پیش‌نیاز

- نامه در وضعیت پیش‌نویس باشد (`Status == Draft`)
    
- کاربر همان `CreatorUserId` باشد
    
- اطلاعات ضروری (گیرنده، متن، عنوان) تکمیل شده باشند
    

---

### ✅ نتیجه موفق

- نامه نهایی می‌شود (`IsFinalized = true`)
    
- وضعیت نامه به `Sent` یا مشابه آن تغییر می‌کند
    
- شماره رسمی نامه (LetterNumber) تولید و ثبت می‌شود
    
- لاگ با عنوان «نهایی‌سازی نامه» ثبت می‌شود
    
- اعلان (Notification) برای گیرنده/واحد مقصد ارسال می‌شود
    

---

### ❌ نتیجه ناموفق

- عدم دسترسی مجاز
    
- اطلاعات ناقص یا نامعتبر
    
- نامه قبلاً نهایی شده است
    

---

### 📥 داده‌های ورودی

|فیلد|نوع|الزامی|توضیح|
|---|---|---|---|
|LetterId|Guid|✅|شناسه نامه موردنظر|

---

### 🧠 منطق عملکرد

1. بررسی مالکیت نامه و Draft بودن آن
    
2. بررسی کامل بودن اطلاعات (گیرنده، عنوان، متن)
    
3. تولید شماره رسمی `LetterNumber` با الگوریتم تعیین‌شده (مثلاً تاریخ + شماره سریال)
    
4. تغییر وضعیت به `Sent` یا معادل آن
    
5. علامت‌گذاری `IsFinalized = true`
    
6. ثبت در `LetterLog` با عنوان "Finalized"
    
7. ایجاد `LetterNotification` برای گیرنده
    
8. بروزرسانی زمان `UpdatedAt`
    

---

### 🔐 ملاحظات امنیتی

- فقط کاربر ایجادکننده می‌تواند نامه را نهایی کند
    
- نامه پس از نهایی‌شدن دیگر قابل ویرایش نیست