|نام فیلد|نوع داده|الزامی؟|توضیحات|
|---|---|---|---|
|`id`|Integer (PK)|✅|شناسه یکتا برای لاگ|
|`letterId`|FK (Letter)|✅|ارتباط با نامه‌ای که این لاگ مربوط به آن است|
|`action`|Enum|✅|نوع عملیات: Created, Edited, Sent, Viewed, Deleted, Forwarded, Replied|
|`actorId`|FK (User)|✅|شناسه کاربر انجام‌دهنده این عمل|
|`actorRole`|String / Enum|❌|نقش کاربر در زمان انجام عملیات (اختیاری)|
|`timestamp`|DateTime|✅|زمان دقیق انجام عملیات|
|`note`|String (nullable)|❌|توضیح تکمیلی یا پیام همراه عملیات|
|`ipAddress`|String|❌|در صورت نیاز به ثبت امنیتی (از طریق پنل یا API یا دستگاه خاص)|


مقادیر پیشنهادی برای فیلد `action`:
public enum LetterLogAction {
    Created,
    Edited,
    Deleted,
    Sent,
    Received,
    Viewed,
    Replied,
    Forwarded,
    Approved,
    Rejected,
    Printed,
    Exported,
    Archived
}

