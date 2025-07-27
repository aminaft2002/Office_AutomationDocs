

# 📄 Entity: Letter (نامه)

## 🎯 هدف
مدل `Letter` نماینده یک نامه‌ی رسمی یا داخلی در سامانه اتوماسیون اداری است. این موجودیت شامل اطلاعات کلی نامه، فرستنده و گیرنده، محتوا، وضعیت و پیوست‌ها می‌باشد.

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





