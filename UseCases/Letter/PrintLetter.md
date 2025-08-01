
| بخش                                                               | توضیح                                                                                                    |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| 🎯 **هدف**                                                        | چاپ نسخه‌ی فیزیکی یک نامه (برای بایگانی، ثبت کاغذی، یا ارسال دستی)                                       |
| 👤 **نقش‌های مجاز**                                               | کاربر دارای مجوز `ViewLetter`                                                                            |
| 📥 **ورودی‌ها**                                                   | `LetterId`, `UserId`                                                                                     |
| 📤 **خروجی‌ها**                                                   | فایل قابل چاپ (HTML یا PDF) یا ارسال به پرینتر کاربر                                                     |
| 🔄 **مراحل اجرای یوزکیس**                                         |                                                                                                          |
| 1️⃣                                                               | دریافت درخواست چاپ با `LetterId` و شناسه کاربر (`UserId`)                                                |
| 2️⃣                                                               | بررسی وجود نامه و مجوز دسترسی کاربر به آن (`CanView`)                                                    |
| 3️⃣                                                               | واکشی اطلاعات کامل نامه شامل: `Subject`, `Body`, `Sender`, `Receiver`, `LetterDate`, `Attachments` و ... |
| 4️⃣                                                               | قالب‌بندی مناسب چاپ (اضافه کردن Header, Footer, شماره نامه، تاریخ، سازمان، و بارکد در صورت نیاز)         |
| 5️⃣                                                               | تولید خروجی HTML یا PDF جهت پیش‌نمایش یا ارسال مستقیم به پرینتر                                          |
| 6️⃣                                                               | ثبت لاگ چاپ (در `LetterLog`) با ذکر `PrintedBy` و `PrintTime`                                            |
| ⚠️ **پیش‌شرط‌ها**                                                 | کاربر باید مجوز مشاهده نامه را داشته باشد                                                                |
| 🔐 **ملاحظات امنیتی**                                             | جلوگیری از چاپ نامه‌های `Confidential` توسط کاربران فاقد مجوز سطح بالا                                   |
| 📚 **موجودیت‌های مرتبط**                                          | `Letter`, `User`, `LetterAttachment`, `LetterLog`, `Unit`                                                |
| 🚀 **قابلیت‌های توسعه آینده**                                     |                                                                                                          |
| - تعریف قالب‌های مختلف چاپ بر اساس نوع نامه (صادره، وارده، داخلی) |                                                                                                          |
| - افزودن QR Code یا امضای دیجیتال گرافیکی                         |                                                                                                          |
| - تعریف سطح دسترسی برای مجاز بودن چاپ                             |                                                                                                          |