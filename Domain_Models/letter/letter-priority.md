
|نام فیلد|نوع داده|الزامی؟|توضیحات|
|---|---|---|---|
|`id`|Integer (PK)|✅|شناسه یکتا|
|`title`|String|✅|عنوان سطح اولویت (مثال: عادی، فوری، خیلی فوری)|
|`description`|String|❌|توضیحات اختیاری درباره‌ی این سطح اولویت|
|`colorCode`|String|❌|کد رنگ برای نمایش بصری در UI (مثال: `#FF0000`)|
|`isActive`|Boolean (default: true)|❌|فعال یا غیرفعال بودن این سطح اولویت|
|`createdAt`|DateTime (auto)|✅|زمان ایجاد رکورد|
|`updatedAt`|DateTime (auto)|✅|زمان آخرین ویرایش رکورد|




### 🔗 ارتباط با دیگر مدل‌ها

- در مدل `letter-entity`، یک کلید خارجی (FK) به `letter-priority.id` به نام `priorityId` وجود خواهد داشت.
- 