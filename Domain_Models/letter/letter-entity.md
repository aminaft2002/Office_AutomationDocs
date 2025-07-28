

# 📄 Entity: Letter (نامه)

## 🎯 هدف
مدل `Letter` نماینده یک نامه‌ی رسمی یا داخلی در سامانه اتوماسیون اداری است. این موجودیت شامل اطلاعات کلی نامه، فرستنده و گیرنده، محتوا، وضعیت و پیوست‌ها می‌باشد.

|فیلد|نوع داده|توضیح|
|---|---|---|
|`Id`|`Guid`|شناسه یکتا|
|`LetterNumber`|`string`|شماره نامه (می‌تواند دستی یا خودکار باشد)|
|`Subject`|`string`|عنوان نامه|
|`Body`|`string` (Text)|متن کامل نامه|
|`SenderUserId`|`Guid?`|کاربری که نامه را فرستاده (در صورت نیاز)|
|`SenderUnitId`|`Guid?`|واحدی که نامه از آن ارسال شده|
|`LetterType`|`enum`|نوع نامه: دریافتی، ارسالی، پیش‌نویس، داخلی، ارجاعی|
|`Priority`|`enum`|عادی، فوری، خیلی فوری|
|`Confidentiality`|`enum`|عادی، محرمانه، خیلی محرمانه|
|`Status`|`enum`|پیش‌نویس، ارسال‌شده، خوانده‌شده، آرشیو شده|
|`RegistrationDate`|`DateTime`|تاریخ ثبت نامه در سیستم|
|`LetterDate`|`DateTime?`|تاریخ درج‌شده در خود نامه|
|`IsFinalized`|`bool`|آیا نامه نهایی شده؟ (غیربرگشت‌پذیر)|
|`CreatorUserId`|`Guid`|کاربر ایجادکننده|
|`CreatedAt`|`DateTime`|زمان ایجاد|
|`UpdatedAt`|`DateTime?`|زمان آخرین ویرایش|

| ارتباط                                        | توضیح |
| --------------------------------------------- | ----- |
| `Letter → User` (SenderUserId, CreatorUserId) |       |
| `Letter → Unit` (SenderUnitId)                |       |
| `Letter → Letter-attachment` (1:N)            |       |
| `Letter → Letter-routing` (1:N)               |       |
| `Letter → Letter-tag` (M:N)                   |       |
| `Letter → Letter-permission` (M:N)            |       |
|                                               |       |

|ویژگی|توضیح|
|---|---|
|`DigitalSignature`|امضای دیجیتال برای اعتبارسنجی نهایی|
|`LetterTemplateId`|در صورت ساخت از یک الگوی نامه|
|`ResponseToLetterId`|شناسه نامه‌ای که این نامه پاسخ آن است|
|`ExternalLetterNumber`|شماره نامه‌ای از سازمان‌های بیرونی|
|`RelatedProjectId`|اتصال نامه به پروژه یا پرونده خاص|

---

## 🧱 فیلدهای اصلی

| فیلد | نوع | توضیح |
|------|-----|-------|
| `Id` | `Guid` | شناسه یکتا |
| `LetterNumber` | `string` | شماره نامه (سیستمی یا دستی) |
| `Type` | `LetterType` | نوع نامه: داخلی، وارده، صادره |
| `Subject` | `string` | موضوع نامه |
| `Body` | `string` | متن اصلی نامه |
| `SenderName` | `string` | نام فرستنده (در نامه صادره یا داخلی) |
| `SenderOrg` | `string` | سازمان فرستنده |
| `ReceiverName` | `string` | نام گیرنده (برای وارده یا داخلی) |
| `ReceiverOrg` | `string` | سازمان گیرنده |
| `LetterDate` | `DateTime` | تاریخ نامه رسمی |
| `RegisterDate` | `DateTime` | تاریخ ثبت در سیستم |
| `IsConfidential` | `bool` | آیا محرمانه است؟ |
| `Status` | `LetterStatus` | وضعیت فعلی نامه |
| `Notes` | `string` | توضیحات داخلی یا توضیح ثبت‌کننده |




  // 🔗 روابط (Foreign Keys / Associations)
  createdBy: User
  organization-unit: Organization-unit
  status: Letter-Status
  priority: Letter-Priority
  type: Letter-Type

  // 🔗 روابط چندگانه
  attachments: Letter-Attachment[]
  permissions: Letter-Permission[]
  routings: Letter-Routing[]
}


---

## 🔁 روابط (در سایر فایل‌ها تعریف می‌شوند)

- `Attachments`: لیست فایل‌های پیوست‌شده ← [letter-attachment.md](letter-attachment.md)
- `Routing`: مسیرهای ارجاع ← [letter-routing.md](letter-routing.md)
- `Permissions`: دسترسی‌های مرتبط ← [letter-permission.md](letter-permission.md)

---
## 🧩 نکات طراحی

- `LetterNumber` ممکن است به‌صورت اتوماتیک و بر اساس الگوی خاص (مثل تاریخ+سریال) تولید شود.
    
- `IsConfidential == true` باعث محدود شدن دسترسی به نامه می‌شود.
    
- تاریخ رسمی (`LetterDate`) با تاریخ ثبت در سیستم (`RegisterDate`) ممکن است متفاوت باشد.
## 🔸 Enums مورد نیاز:

```csharp
enum LetterType {
  Internal,
  Incoming,
  Outgoing
}

enum LetterStatus {
  Draft,
  InProgress,
  Referred,
  Responded,
  Closed
}





