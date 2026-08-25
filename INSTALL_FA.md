# راهنمای نصب پلتفرم هوشمند امکان‌سنجی صادرات پالایش نفت جی

## روش پیشنهادی: اجرای کامل با Docker

پیش‌نیاز: نصب Docker Desktop روی ویندوز یا Docker Engine به‌همراه Docker Compose روی لینوکس.

1. فایل ZIP را از حالت فشرده خارج کنید.
2. ترمینال را در پوشه `Jey-Oil-Export-Intelligence` باز کنید.
3. دستور زیر را اجرا کنید:

```bash
docker compose up --build
```

4. پس از آماده‌شدن سرویس‌ها، آدرس‌های زیر در دسترس هستند:

- داشبورد: `http://localhost:3000`
- مستندات API: `http://localhost:8000/docs`
- PostgreSQL: پورت `5432`

برای توقف:

```bash
docker compose down
```

برای توقف و حذف دیتابیس محلی نیز می‌توان از `docker compose down -v` استفاده کرد؛ این دستور داده‌های ذخیره‌شده را حذف می‌کند.

## اجرای بدون Docker برای توسعه

### فرانت‌اند

```bash
cp .env.example .env
npm install
npm run dev -- --host 0.0.0.0 --port 3000
```

### بک‌اند

در پوشه `backend` فایل `.env.example` را به `.env` تبدیل کرده، سپس:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

در ویندوز، فعال‌سازی محیط پایتون با `.venv\Scripts\activate` انجام می‌شود.

## نسخه HTML آفلاین

فایل `offline-html/index.html` را مستقیماً با مرورگر باز کنید. این نسخه برای نمایش و محاسبات اولیه طراحی شده و به دیتابیس، ذخیره سناریو و APIهای زنده متصل نیست.

## نکات امنیتی و داده‌ای

- گذرواژه نمونه PostgreSQL را پیش از استقرار سازمانی تغییر دهید.
- کلیدها و اطلاعات دسترسی ITC را در کد فرانت‌اند قرار ندهید.
- اعداد نمونه با داده واقعی اشتباه گرفته نشوند.
- برای استقرار عمومی از HTTPS، مدیریت Secrets، پشتیبان‌گیری دیتابیس و احراز هویت سازمانی استفاده کنید.
