# Django Blog Deployment Guide

Your project is now ready for deployment! Here are several options to deploy your Django blog online.

## 🚀 Quick Deployment Options

### Option 1: PythonAnywhere (Easiest - Free Tier Available)

**Best for:** Beginners, free hosting with minimal setup

1. **Create Account**
   - Go to https://www.pythonanywhere.com
   - Sign up for a free account

2. **Upload Your Code**
   - Open a Bash console
   - Clone or upload your project:
     ```bash
     git clone <your-repo-url>
     # OR upload files via Files tab
     ```

3. **Set Up Virtual Environment**
   ```bash
   mkvirtualenv --python=/usr/bin/python3.10 myblog
   cd ~/myblog
   pip install -r requirements.txt
   ```

4. **Configure Web App**
   - Go to Web tab → Add a new web app
   - Choose Manual configuration → Python 3.10
   - Set source code: `/home/yourusername/myblog`
   - Set working directory: `/home/yourusername/myblog`
   - Edit WSGI file and add:
     ```python
     import sys
     path = '/home/yourusername/myblog'
     if path not in sys.path:
         sys.path.append(path)
     
     from myblog.wsgi import application
     ```

5. **Set Up Static Files**
   - In Web tab, add static files mapping:
   - URL: `/static/`
   - Directory: `/home/yourusername/myblog/staticfiles`

6. **Run Migrations**
   ```bash
   python manage.py migrate
   python manage.py createsuperuser
   python manage.py collectstatic
   ```

7. **Reload** your web app and visit your URL!

---

### Option 2: Render (Free Tier - Modern & Easy)

**Best for:** Modern deployment, automatic builds from Git

1. **Prepare Git Repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```
   Push to GitHub, GitLab, or Bitbucket

2. **Sign Up at Render**
   - Go to https://render.com
   - Sign up and connect your Git account

3. **Create Web Service**
   - Click "New +" → "Web Service"
   - Connect your repository
   - Configure:
     - **Name:** myblog
     - **Environment:** Python 3
     - **Build Command:** `pip install -r requirements.txt && python manage.py collectstatic --noinput && python manage.py migrate`
     - **Start Command:** `gunicorn myblog.wsgi`

4. **Add Environment Variables**
   - `PYTHON_VERSION`: `3.13.2`
   - `SECRET_KEY`: Generate a new secret key
   - `DEBUG`: `False`

5. **Deploy** - Render will automatically build and deploy!

---

### Option 3: Railway (Free Trial - Very Easy)

**Best for:** Quick deployment with databases included

1. **Install Railway CLI** (optional)
   ```bash
   npm install -g @railway/cli
   ```

2. **Sign Up**
   - Go to https://railway.app
   - Sign up with GitHub

3. **Deploy via GitHub**
   - Create a new project
   - Choose "Deploy from GitHub repo"
   - Select your repository
   - Railway auto-detects Django

4. **Add Environment Variables**
   - In Variables tab:
     - `DEBUG`: `False`
     - `SECRET_KEY`: Your secret key

5. **Deploy automatically** on each push!

---

### Option 4: Fly.io (Free Tier Available)

**Best for:** Global deployment with CDN

1. **Install Flyctl**
   ```bash
   # Windows (PowerShell)
   iwr https://fly.io/install.ps1 -useb | iex
   ```

2. **Launch App**
   ```bash
   fly auth signup
   cd /path/to/myblog
   fly launch
   ```

3. **Configure** when prompted:
   - App name: myblog
   - Region: Choose closest to you
   - Database: Choose SQLite or PostgreSQL

4. **Deploy**
   ```bash
   fly deploy
   ```

---

## 📝 Pre-Deployment Checklist

Before deploying to production:

### 1. Update Settings for Production

Edit `myblog/settings.py`:

```python
import os

# Generate new SECRET_KEY for production
SECRET_KEY = os.environ.get('SECRET_KEY', 'your-secret-key-here')

# Turn off DEBUG in production
DEBUG = os.environ.get('DEBUG', 'False') == 'True'

# Add your domain
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com', '.railway.app', '.fly.dev', '.pythonanywhere.com']
```

### 2. Collect Static Files

```bash
python manage.py collectstatic
```

### 3. Run Migrations

```bash
python manage.py migrate
```

### 4. Create Superuser

```bash
python manage.py createsuperuser
```

### 5. Test Locally with Production Settings

```bash
DEBUG=False python manage.py runserver
```

---

## 🔒 Security Recommendations

1. **Never commit secrets** - Use environment variables
2. **Use strong SECRET_KEY** - Generate new one for production
3. **Set DEBUG=False** in production
4. **Configure ALLOWED_HOSTS** with your actual domain
5. **Use HTTPS** - Most platforms provide it free
6. **Regular backups** of your database

---

## 🗃️ Database Options

### SQLite (Default - Good for Small Sites)
- Already configured
- File-based, simple
- Limited to single server

### PostgreSQL (Recommended for Production)
Most platforms offer PostgreSQL:
- More robust and scalable
- Better for concurrent users
- Easy to set up on Render/Railway

To use PostgreSQL, install:
```bash
pip install psycopg2-binary
```

Update settings.py:
```python
import dj_database_url

DATABASES = {
    'default': dj_database_url.config(
        default='sqlite:///db.sqlite3',
        conn_max_age=600
    )
}
```

---

## 🆘 Common Issues

### Static files not loading?
- Run `python manage.py collectstatic`
- Check STATIC_ROOT and STATIC_URL settings
- Verify static files mapping in your platform

### Database errors?
- Run `python manage.py migrate`
- Check database connection settings
- Ensure database is created

### 500 Server Error?
- Set DEBUG=True temporarily to see errors
- Check server logs
- Verify all environment variables are set

---

## 📚 Additional Resources

- [Django Deployment Checklist](https://docs.djangoproject.com/en/6.0/howto/deployment/checklist/)
- [PythonAnywhere Django Tutorial](https://help.pythonanywhere.com/pages/DeployExistingDjangoProject/)
- [Render Django Guide](https://render.com/docs/deploy-django)
- [Railway Django Guide](https://docs.railway.app/guides/django)

---

## ✅ After Deployment

1. Visit your site URL
2. Go to `/admin/` and log in
3. Create your first blog post
4. Share your blog with the world! 🎉

Choose the option that works best for you. **PythonAnywhere** is recommended for absolute beginners, while **Render** and **Railway** offer modern, Git-based workflows.
