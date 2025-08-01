| بخش                                                                   | توضیح                                                                      |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| 🎯 **هدف**                                                            | فعال‌سازی مجدد یک یادداشت که قبلاً به‌صورت soft-delete حذف شده بود         |
| 👤 **نقش‌های مجاز**                                                   | فقط کاربری که یادداشت را ثبت کرده                                          |
| 📥 **ورودی‌ها**                                                       | `NoteId`, `UserId` (از توکن)                                               |
| 📤 **خروجی‌ها**                                                       | پیام موفقیت یا خطا                                                         |
| 🔄 **مراحل اجرای یوزکیس**                                             |                                                                            |
| 1️⃣                                                                   | دریافت `NoteId` و `UserId`                                                 |
| 2️⃣                                                                   | واکشی یادداشت و بررسی مالکیت توسط `UserId`                                 |
| 3️⃣                                                                   | اگر `IsDeleted = true`، مقداردهی: `IsDeleted = false` و `DeletedAt = null` |
| 4️⃣                                                                   | ذخیره تغییرات در دیتابیس                                                   |
| ⚠️ **پیش‌شرط‌ها**                                                     | یادداشت باید حذف شده باشد (`IsDeleted = true`) و متعلق به کاربر فعلی باشد  |
| 🔐 **ملاحظات امنیتی**                                                 | فقط مالک یادداشت مجاز به بازیابی آن است                                    |
| 📚 **موجودیت‌های مرتبط**                                              | `LetterNote`, `User`, `Letter`                                             |
| 🧩 **نکات پیاده‌سازی**                                                |                                                                            |
| - این عمل فقط برای یادداشت‌هایی که soft-delete شده‌اند فعال است       |                                                                            |
| - باید مطمئن شد که `DeletedAt` به null بازگردد تا در فیلترها دیده شود |                                                                            |
| - اگر یادداشت از ابتدا حذف نشده باشد، پیام مناسب نمایش داده شود       |                                                                            |