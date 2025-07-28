#### 🎯 هدف:

برقراری ارتباط چند-به-چند بین برچسب‌ها و نامه‌ها.

|فیلد|نوع داده|کلید|توضیح|
|---|---|---|---|
|`Id`|`Guid`|Primary Key|شناسه یکتا|
|`LetterId`|`Guid`|Foreign Key → Letter.Id|ارجاع به نامه|
|`TagId`|`Guid`|Foreign Key → LetterTag.Id|ارجاع به برچسب|

---

### 🔁 روابط

- `Letter → LetterTag` (Many-to-Many via LetterTagAssignment)
    
- `LetterTagAssignment → Letter`
    
- `LetterTagAssignment → LetterTag`