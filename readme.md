How to use this repo:

Prerequisites

Make sure the following are installed on your system:

- Python 3.x
- pip (Python package manager)
- PostgreSQL (ensure `psql` is in your PATH)
- Git

1. Clone the Repository

`git clone https://github.com/your-username/your-repo-name.git`
`cd your-repo-name`

2. Set Up Python Environment

`python -m venv venv`
`venv\Scripts\activate`  # On Windows

# OR

`source venv/bin/activate`  # On Mac/Linux
`pip install -r requirements.txt`

3. Create PostgreSQL Database and User
Open your PostgreSQL shell (psql) and run the following:

`CREATE DATABASE my_database;`
`CREATE USER admin WITH PASSWORD 'your-password';`
`GRANT ALL PRIVILEGES ON DATABASE my_database TO admin;`

4. Restore the Database Backup
From your terminal in the project folder, run:

`psql -U admin -d my_database -h localhost -f db_backup.sql`

5. Update Django Settings
In `testproject/settings.py`, update the DATABASES section:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'my_database',
        'USER': 'admin',
        'PASSWORD': 'your-password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

6. Run Migrations (Optional if backup was successful)

`python manage.py migrate`

7. Start the Development Server
`python manage.py runserver`
Visit http://127.0.0.1:8000 in your browser to view the app.
