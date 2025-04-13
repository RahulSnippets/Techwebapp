# Nikoji Technologies Website

A multi-page industrial automation company website built with Django, plain HTML/CSS, and PostgreSQL database.

## Local Development Setup (VS Code)

### Prerequisites

- Python 3.10 or higher
- PostgreSQL database
- Git (optional but recommended)
- Visual Studio Code

### Step 1: Clone or Download the Repository

```bash
git clone <repository-url>
# or download and extract the ZIP file
```

### Step 2: Set Up Python Environment

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure Database

1. Create a PostgreSQL database
2. Create a `.env` file in the root directory with the following content:

```
DEBUG=True
SECRET_KEY=your_secret_key_here
DATABASE_URL=postgres://username:password@localhost:5432/database_name
ALLOWED_HOSTS=localhost,127.0.0.1
```

### Step 5: Run Migrations

```bash
cd nikoji_tech
python manage.py migrate
```

### Step 6: Create Superuser (Admin)

```bash
python manage.py createsuperuser
```

### Step 7: Run the Development Server

```bash
python manage.py runserver
```

Access the website at: http://127.0.0.1:8000/  
Access the admin panel at: http://127.0.0.1:8000/admin/

### VS Code Extensions Recommended

- Python
- Django
- PostgreSQL
- SQLTools
- Better Comments
- HTML CSS Support
- Auto Close Tag
- GitLens

## cPanel Deployment Instructions

### Step 1: Prepare Your Code

1. Update settings for production:
   - Set `DEBUG = False` in settings.py
   - Update `ALLOWED_HOSTS` to include your domain
   - Configure static files settings

2. Export your local database (optional):
   ```bash
   python manage.py dumpdata > db_backup.json
   ```

### Step 2: Create a ZIP Archive

1. Include only necessary files:
   - nikoji_tech/ (entire directory)
   - requirements.txt
   - passenger_wsgi.py
   - .htaccess (if needed)
   - README.md
   
2. Exclude unnecessary files:
   - venv/ (virtual environment)
   - *.pyc files
   - __pycache__ directories
   - .git directory
   - any local configuration files

### Step 3: Upload to cPanel

1. Log in to your cPanel account
2. Navigate to File Manager
3. Upload the ZIP file to your domain's root directory
4. Extract the ZIP file

### Step 4: Set Up Python Application

1. In cPanel, go to "Setup Python App"
2. Configure your application:
   - Python version: 3.10 or higher
   - Application root: /path/to/your/nikoji_tech
   - Application URL: your domain or subdomain
   - Application startup file: passenger_wsgi.py
   - Application Entry point: application
   
3. Create a virtual environment in cPanel

### Step 5: Install Dependencies

1. Access the Shell via Terminal in cPanel
2. Navigate to your application directory
3. Run: 
   ```bash
   pip install -r requirements.txt
   ```

### Step 6: Configure Database in cPanel

1. Create a new PostgreSQL database in cPanel
2. Create a database user and assign it to the database
3. Update the DATABASE_URL in your production settings to use the cPanel database credentials

### Step 7: Run Migrations and Create Superuser

```bash
cd nikoji_tech
python manage.py migrate
python manage.py createsuperuser
```

### Step 8: Collect Static Files

```bash
python manage.py collectstatic
```

### Step 9: Configure the passenger_wsgi.py File

The `passenger_wsgi.py` file is already included in the codebase and properly configured.

### Step 10: Restart the Application

1. In cPanel, go to "Setup Python App"
2. Click on your application
3. Click "Restart" button

### Step 11: Configure SSL (Recommended)

1. In cPanel, find "SSL/TLS" or "Let's Encrypt SSL"
2. Follow the process to secure your domain with an SSL certificate

## Database Backup

To back up your PostgreSQL database:

```bash
# On local development or via cPanel terminal
cd nikoji_tech
python manage.py dumpdata > database_backup.json

# To restore the data
python manage.py loaddata database_backup.json
```

## Troubleshooting

### Common Issues and Solutions

1. **Static Files Not Loading**
   - Check your `STATIC_URL` and `STATIC_ROOT` settings
   - Run `python manage.py collectstatic` again
   - Verify permissions on static files directory

2. **Database Connection Issues**
   - Verify database credentials in settings
   - Check if PostgreSQL service is running
   - Ensure the database user has proper permissions

3. **500 Server Error**
   - Check the server logs for detailed error messages
   - Verify that DEBUG is set to False in production
   - Ensure all dependencies are correctly installed

4. **Permission Issues**
   - Check file permissions for your application files (typically 644 for files, 755 for directories)
   - Make sure passenger_wsgi.py has execute permissions (755)

## Maintenance

1. **Regular Backups**
   - Schedule regular database backups
   - Keep backups of your media files

2. **Updates**
   - Regularly update Django and dependencies
   - Monitor security announcements for Django

3. **Performance Monitoring**
   - Use cPanel resource monitoring tools
   - Implement Django Debug Toolbar in development

## Contact

For support or questions, please contact:
- Email: support@nikojitechnologies.com
- Website: https://www.nikojitechnologies.com/contact