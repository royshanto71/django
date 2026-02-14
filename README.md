# My Blog - Django Project

A simple Django blog website with a clean and minimal design.

## Features

- Blog post listing on home page
- Individual post detail pages
- Admin panel for managing posts
- Clean and responsive design
- Author attribution and timestamps

## Project Structure

```
myblog/             # Main project configuration
blog/              # Blog application
  ├── models.py    # Post model
  ├── views.py     # View functions
  ├── admin.py     # Admin configuration
  ├── urls.py      # URL routes
  └── templates/   # HTML templates
      └── blog/
          ├── base.html
          ├── home.html
          └── post_detail.html
```

## Getting Started

### 1. Create a superuser for admin access

```bash
python manage.py createsuperuser
```

Follow the prompts to set up your admin username, email, and password.

### 2. Run the development server

```bash
python manage.py runserver
```

### 3. Access the application

- **Blog Home**: http://127.0.0.1:8000/
- **Admin Panel**: http://127.0.0.1:8000/admin/

### 4. Create your first blog post

1. Go to the admin panel (http://127.0.0.1:8000/admin/)
2. Log in with your superuser credentials
3. Click on "Posts" under the BLOG section
4. Click "Add Post" button
5. Fill in the title and content
6. Select an author (your superuser account)
7. Click "Save"

Your post will now appear on the home page!

## Model Structure

### Post Model

- **title**: The post title (max 200 characters)
- **content**: The main content of the post (text field)
- **author**: Foreign key to User model
- **created_at**: Automatic timestamp when post is created
- **updated_at**: Automatic timestamp when post is modified

## Customization

You can customize the blog by:

- Editing templates in `blog/templates/blog/`
- Modifying styles in `base.html`
- Adding new fields to the Post model
- Creating new views and URL patterns

## Next Steps

Some ideas to extend this blog:

- Add categories or tags
- Enable comments
- Add a search feature
- Create a rich text editor
- Add image uploads
- Implement pagination
- Add user registration

Enjoy your blog!
