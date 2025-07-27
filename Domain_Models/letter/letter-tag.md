|نام فیلد|نوع داده|الزامی؟|توضیحات|
|---|---|---|---|
|`id`|Integer (PK)|✅|شناسه یکتا|
|`title`|String|✅|عنوان برچسب (مثال: محرمانه، نیاز به اقدام، داخلی، فوری و ...)|
|`description`|String|❌|توضیح بیشتر درباره این برچسب|
|`colorCode`|String|❌|کد رنگ مخصوص برای نمایش بصری برچسب در UI|
|`isSystemTag`|Boolean|❌|مشخص می‌کند که آیا این برچسب سیستمی است و کاربر نمی‌تواند حذف کند|
|`isActive`|Boolean (default: true)|❌|برچسب فعال یا غیرفعال|
|`createdAt`|DateTime (auto)|✅|زمان ایجاد|
|`updatedAt`|DateTime (auto)|✅|زمان آخرین به‌روزرسانی|

### 🔗 ارتباط‌ها:

- یک نامه می‌تواند **چندین تگ** داشته باشد ⇒ رابطه Many-to-Many بین `letter-entity` و `letter-tag`
    
- نیاز به جدول واسط: `letter_tag_map`
- 