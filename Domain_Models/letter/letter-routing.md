
# 🔁 Entity: LetterRouting (گردش نامه)

## 🎯 هدف
مدل `LetterRouting` ثبت می‌کند که یک نامه در چه تاریخی، توسط چه کسی، به چه شخص دیگری ارجاع داده شده و وضعیت آن در مسیر گردش چگونه بوده است.

---

## 🧱 فیلدهای اصلی

| فیلد | نوع | توضیح |
|------|-----|--------|
| `Id` | `Guid` | شناسه یکتا |
| `LetterId` | `Guid` | شناسه نامه مربوطه (ارتباط با `Letter`) |
| `FromUserId` | `Guid` | شناسه کاربر فرستنده ارجاع |
| `ToUserId` | `Guid` | شناسه کاربر گیرنده ارجاع |
| `SentAt` | `DateTime` | تاریخ ارسال ارجاع |
| `ReadAt` | `DateTime?` | تاریخ خوانده شدن نامه (nullable) |
| `Note` | `string` | توضیح ارجاع‌دهنده برای گیرنده |
| `Priority` | `int` | اولویت ارجاع (۱ بالا، ۲ متوسط، ۳ پایین) |
| `Status` | `RoutingStatus` | وضعیت ارجاع (در انتظار، خوانده شده، پاسخ داده شده و...) |


|رابطه|نوع ارتباط|توضیح|
|---|---|---|
|`LetterRouting → Letter`|Many-to-One|ارجاع مربوط به کدام نامه است|
|`LetterRouting → FromUser`|Many-to-One|کاربری که نامه را ارجاع داده|
|`LetterRouting → ToUser`|Many-to-One|کاربری که نامه به او ارجاع شده|
|`LetterRouting → FromUnit`|Many-to-One|واحد ارجاع‌دهنده|
|`LetterRouting → ToUnit`|Many-to-One|واحد ارجاع‌شونده|
|`LetterRouting → ActionType`|Enum|نوع ارجاع (ارجاع برای اقدام، اطلاع، بایگانی و...)|
|`LetterRouting → Status`|Enum|وضعیت ارجاع (در انتظار، انجام شده، رد شده)|
|`LetterRouting → ParentRouting`|Optional Self-Reference|اگر ارجاعی در پاسخ به ارجاع قبلی انجام شده باشد|




|رابطه|نوع ارتباط|توضیح|
|---|---|---|
|`LetterRouting → Letter`|Many-to-One|مربوط به کدام نامه|
|`LetterRouting → User`|Many-to-One|فرستنده و گیرنده (User)|
|`LetterRouting → Unit`|Many-to-One|فرستنده و گیرنده (Unit)|
|`LetterRouting → User`|Many-to-One|کاربر ایجادکننده|



---
## 📦 وابستگی‌های اصلی

- `User` ← برای `FromUserId`, `ToUserId`
    
- `Unit` ← برای `FromUnitId`, `ToUnitId`
    
- `Letter` ← برای `LetterId`
    
- `RoutingStatus` ← وضعیت ارجاع
    
- `RoutingAction` ← نوع اقدام مورد انتظار
    

---

## 🧠 نکات مهم طراحی

- **Self-Reference** برای امکان ایجاد زنجیره ارجاعات.
    
- **زمان پاسخ‌دهی، کامنت و مهر مشاهده** در فیلدهای موجود در مدل پایه (در دامین) در نظر گرفته شده است.
    
- فقط یکی از ارجاعات می‌تواند به عنوان **ارجاع نهایی‌کننده (IsFinal)** در نظر گرفته شود.
## 📌 نکات طراحی

- اگر `ReadAt` مقدار داشته باشد، یعنی گیرنده نامه را دیده است.
    
- هر `Letter` می‌تواند دارای چندین `LetterRouting` باشد (لیست مسیرها)
    
- در نامه‌های محرمانه، ممکن است `FromUserId` مخفی نمایش داده شود
## 🔸 Enum مورد نیاز:

```csharp
enum RoutingStatus {
  Pending,
  Read,
  Responded,
  Forwarded
}
