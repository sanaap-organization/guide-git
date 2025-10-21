# guide-git

## 🚀 Gitflow & Commit Convention Guide  
**راهنمای حرفه ای Git Workflow و نوشتن Commit**

## 🧭 مقدمه

این فایل توضیح میده چطور با استفاده از **Gitflow strategy** و **Conventional Commits** میشه یک پروژه حرفه ای و منظم داشت.  
هدف اینه که تمام اعضای تیم با ساختار یکسان کار کنن تا **تاریخچه commit ها تمیز و قابل پیگیری** بمونه.

## 🌿 Gitflow چیست

Gitflow یک مدل برای مدیریت branch ها در پروژه است که کمک میکنه توسعه، تست و انتشار نسخه ها کاملاً ساختارمند انجام بشه.

### 📊 ساختار اصلی branch ها

| Branch | وظیفه | توضیح |
|--------|--------|--------|
| `main` | نسخه پایدار | کدهایی که در محیط production منتشر شدن |
| `develop` | branch توسعه | آخرین تغییرات تایید شده برای نسخه بعد |
| `feature/*` | قابلیت جدید | از develop ساخته میشه و بعد از اتمام به develop merge میشه |
| `bugfix/*` | رفع باگ در توسعه | از develop ساخته و به اون برگردونده میشه |
| `release/*` | آماده سازی نسخه جدید | از develop ساخته میشه و بعد از تست به main و develop merge میشه |
| `hotfix/*` | رفع باگ اضطراری در نسخه منتشر شده | از main ساخته میشه و بعد از اصلاح به main و develop merge میشه |

### 🪄 مثال از فلو توسعه

```bash
git checkout develop
git checkout -b feature/add-login
git add .
git commit -m "feat(auth): add login endpoint and validation"
git checkout develop
git merge --no-ff feature/add-login
git branch -d feature/add-login
```

## 🧩 الگوی نامگذاری branch ها

| نوع | الگو | مثال |
|------|------|------|
| Feature | `feature/<short-description>` | `feature/add-login-api` |
| Bugfix | `bugfix/<short-description>` | `bugfix/fix-token-refresh` |
| Hotfix | `hotfix/<short-description>` | `hotfix/fix-prod-500` |
| Release | `release/<version>` | `release/1.3.0` |

> فقط از حروف کوچک و dash استفاده کن  
> فاصله و underscore مجاز نیست

## 💬 ساختار Commit Message

در این پروژه از استاندارد **Conventional Commits** استفاده میشه که باعث میشه commit history تمیز، قابل فهم و خودکار برای changelog باشه.

### 📘 ساختار کلی

```
<type>(<scope>): <subject>

<body>

<footer>
```

### 🧩 توضیحات اجزا

| بخش | توضیح |
|------|------|
| **type** | نوع تغییر مثل feat, fix, docs و ... |
| **scope** | محدوده تغییر (اختیاری اما پیشنهاد میشود) |
| **subject** | توضیح کوتاه تغییر |
| **body** | توضیحات کاملتر در صورت نیاز |
| **footer** | ارجاع به issue یا توضیح breaking changes (اختیاری) |

### 🔖 انواع type ها

| Type | معنی | مثال |
|------|------|------|
| `feat` | قابلیت جدید | `feat(auth): add JWT login` |
| `fix` | رفع باگ | `fix(api): resolve token expiration issue` |
| `docs` | تغییر در مستندات | `docs(readme): add setup section` |
| `style` | تغییر ظاهری یا formatting | `style(lint): fix spacing` |
| `refactor` | بازنویسی بدون تغییر عملکرد | `refactor(models): simplify user serializer` |
| `perf` | بهبود عملکرد | `perf(cache): optimize redis queries` |
| `test` | اضافه کردن تست | `test(api): add auth middleware tests` |
| `chore` | کارهای جانبی مثل dependency یا CI/CD | `chore(deps): update django to 4.2` |
| `revert` | بازگرداندن commit قبلی | `revert: revert "feat(auth): add login"` |

### 📗 مثال های خوب

```
feat(auth): implement OAuth2 login with Google

- Added new /auth/google endpoint
- Updated user model to store external ID
- Added GOOGLE_CLIENT_ID and GOOGLE_SECRET env vars
```

## 🔄 Pull Request Workflow

1. قبل از Pull Request
   - تست ها رو اجرا کن
   - lint رو اجرا کن
   - commit ها باید تمیز و معنی دار باشن
2. در Pull Request
   - عنوان واضح بنویس
   - توضیح بده چه تغییری کردی و چرا
3. بعد از Merge
   - branch رو حذف کن
   - changelog رو آپدیت کن

## 📦 مثال از فلو واقعی

```bash
git checkout develop
git checkout -b feature/add-user-profile
git add .
git commit -m "feat(user): add profile endpoint"
git commit -m "fix(user): correct serializer"
git push origin feature/add-user-profile
git branch -d feature/add-user-profile
```

## 🧠 نکات حرفه ای

- هر commit باید مستقل و قابل تست باشد  
- commit های نامرتبط را در یک PR نگذار  
- هر feature branch فقط برای یک هدف مشخص باشد  
- همیشه قبل از شروع git pull develop انجام بده  
- از git rebase -i برای تمیز کردن commit history استفاده کن  

## ⚡ خلاصه سریع

✅ Branch: `feature/add-login-api`  
✅ Commit: `feat(auth): add JWT login`  
✅ PR Title: `Add JWT login to authentication module`  
✅ بعد از merge: حذف branch  
✅ قبل از push: تست و lint  
