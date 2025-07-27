| نام فیلد       | نوع داده       | الزامی؟ | توضیحات                                      |
| -------------- | -------------- | ------- | -------------------------------------------- |
| `id`           | Integer (PK)   | ✅       | شناسه یکتا                                   |
| `parentId`     | FK (Letter)    | ✅       | نامه‌ای که این پاسخ به آن داده شده           |
| `replyBy`      | FK (User)      | ✅       | کاربری که پاسخ داده                          |
| `replyContent` | Text / HTML    | ✅       | متن پاسخ                                     |
| `timestamp`    | DateTime       | ✅       | زمان پاسخ                                    |
| `attachments`  | List<FK(File)> | ❌       | فایل‌های ضمیمه پاسخ                          |
| `status`       | Enum           | ❌       | وضعیت پاسخ: Draft, Final, Approved, Rejected |