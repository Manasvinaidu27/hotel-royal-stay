# Hotel Royal Stay — Vercel Deployment Checklist

## 1. Local verification

```bash
python manage.py check
python manage.py migrate
python manage.py runserver
```

Test the home page, rooms, login/register, and admin locally.

## 2. Vercel environment variables

Set these in Vercel Project Settings → Environment Variables:

- `DJANGO_SECRET_KEY` = a strong production secret
- `DEBUG` = `False`
- `ALLOWED_HOSTS` = your Vercel hostname, for example `your-project.vercel.app`
- `CSRF_TRUSTED_ORIGINS` = `https://your-project.vercel.app`
- `DATABASE_URL` = your production PostgreSQL connection string
- `RAZORPAY_KEY_ID` = your Razorpay key
- `RAZORPAY_KEY_SECRET` = your Razorpay secret

If you add a custom domain, include that domain in `ALLOWED_HOSTS` and its HTTPS origin in `CSRF_TRUSTED_ORIGINS`.

## 3. Database

The settings file keeps SQLite as the local fallback and automatically uses `DATABASE_URL` when it is supplied. Configure PostgreSQL before running production migrations/seed data.

## 4. Important for uploads

Vercel deployments should not be used as permanent local storage for user-uploaded media such as ID proofs or room images. Use persistent object storage for production uploads.

## 5. Vercel

The project already contains `manage.py` and the Django WSGI entry point. Current Vercel Django support can detect the Django application structure without requiring an `/api` folder or a `vercel.json` solely for Django routing.
