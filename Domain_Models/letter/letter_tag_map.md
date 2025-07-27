
|نام فیلد|نوع داده|الزامی؟|توضیحات|
|---|---|---|---|
|`id`|Integer (PK)|✅|شناسه یکتا|
|`letterId`|FK to `letter-entity.id`|✅|شناسه نامه|
|`tagId`|FK to `letter-tag.id`|✅|شناسه برچسب|
|`createdAt`|DateTime|✅|زمان افزودن این تگ به نامه|
