

|بخش|توضیح|
|---|---|
|🎯 **هدف**|ارسال گروهی یک نامه مشابه به چند واحد یا کاربر به‌صورت هم‌زمان|
|👤 **نقش‌های مجاز**|کاربران دارای مجوز `SendLetter` و `SelectMultipleRecipients`|
|📥 **ورودی‌ها**|`LetterTemplateId` یا `LetterDraftId`, لیست `ReceiverIds` (کاربران یا واحدها), `SenderUserId`|
|📤 **خروجی‌ها**|لیست نامه‌های ارسال‌شده با شناسه‌های یکتا (LetterIds) و وضعیت ارسال|
|🔄 **مراحل اجرای یوزکیس**||
|1️⃣|دریافت درخواست ارسال گروهی با استفاده از الگو یا پیش‌نویس موجود|
|2️⃣|بررسی اعتبار دسترسی کاربر و وجود نامه اولیه (Draft/Template)|
|3️⃣|واکشی محتوا و متادیتای نامه مبنا (مانند: `Subject`, `Body`, `Priority`, `Confidentiality`)|
|4️⃣|تکرار برای هر گیرنده: ایجاد یک نسخه جدید از نامه با گیرنده‌ی خاص و ثبت در دیتابیس|
|5️⃣|ثبت هر مورد در جدول `Letter`, `LetterRouting`, و `LetterLog`|
|6️⃣|بروزرسانی داشبورد گیرندگان و ایجاد نوتیفیکیشن در `LetterNotification`|
|7️⃣|بازگشت لیست `LetterIds` موفق و موارد دارای خطا (در صورت وجود)|
|⚠️ **پیش‌شرط‌ها**|نامه مبنا باید نهایی یا قابل ارسال باشد و کاربر اجازه ارسال به چند نفر را داشته باشد|
|🔐 **ملاحظات امنیتی**||
|- بررسی سطوح دسترسی به گیرندگان (ممکن است برخی گیرندگان نیاز به تأییدیه داشته باشند)||
|- در صورت محرمانه بودن نامه، محدود کردن دریافت‌کنندگان بر اساس Clearance سطح دسترسی||
|📚 **موجودیت‌های مرتبط**|`Letter`, `User`, `Unit`, `LetterTemplate`, `LetterRouting`, `LetterNotification`, `LetterLog`|
|🚀 **قابلیت‌های توسعه آینده**||
|- افزودن زمان‌بندی برای ارسال گروهی در آینده (`BulkSendSchedule`)||
|- گزارش‌گیری از نتایج ارسال (چاپ شده/خوانده شده/ارجاع شده)||
|- قابلیت Undo برای لغو ارسال‌های اشتباه در مدت کوتاه پس از ارسال||