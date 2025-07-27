| فیلد             | نوع داده                   | توضیح                            |
| ---------------- | -------------------------- | -------------------------------- |
| `id`             | Integer                    | شناسه                            |
| `templateId`     | FK to `letter-template.id` | ارتباط با قالب مربوطه            |
| `placeholderKey` | String                     | نام متغیر (مثال: `ReceiverName`) |
| `defaultValue`   | String                     | مقدار پیش‌فرض اگر داده‌ای نبود   |
| `description`    | String                     | توضیح برای کاربر / مدیر سیستم    |