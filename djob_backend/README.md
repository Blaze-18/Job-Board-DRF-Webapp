
```markdown
# Djob Backend

The backend of **Djob** is built using **Django REST Framework**. It provides a RESTful API for managing users, jobs, and job applications. The backend handles authentication, job posting, editing, deletion, and searching.

---

## 🧰 How It Works

1. **Models:** The backend defines models such as `Job` and `User` to structure data.
2. **Serializers:** Models are serialized to JSON for API responses.
3. **Views & API Endpoints:** DRF views handle CRUD operations for jobs and users.
4. **Routing:** `urls.py` maps endpoints to the views.
5. **Database:** SQLite is used for data storage in the prototype version.

---

## 🚀 Technology Stack

- **Backend Framework:** Django REST Framework
- **Language:** Python 3.11+
- **Database:** SQLite (prototype)
- **Authentication:** Token-based authentication
- **API Tools:** Django serializers for JSON responses

---

## 📦 Folder Structure

```

djob\_backend/
├── manage.py
├── db.sqlite3
├── djob\_backend/
│   ├── **init**.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── job/
├── **init**.py
├── admin.py
├── apps.py
├── forms.py
├── models.py
├── serializers.py
├── tests.py
├── urls.py
└── views.py

````

---

## 🔗 API Endpoints

### Jobs
- `GET /api/v1/jobs/` – List all jobs
- `GET /api/v1/jobs/<id>/` – Retrieve a single job
- `POST /api/v1/jobs/create/` – Create a job (requires authentication)
- `PUT /api/v1/jobs/<id>/update/` – Update a job (requires authentication)
- `DELETE /api/v1/jobs/<id>/delete/` – Delete a job (requires authentication)

### Categories
- `GET /api/v1/jobs/categories/` – List all job categories

### Authentication
- `POST /api/v1/auth/login/` – Login user
- `POST /api/v1/auth/register/` – Register user

---

## 💻 Installation

```bash
# Clone repository
git clone <repository-url>
cd djob_backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Migrate database
python manage.py migrate

# Create admin user
python manage.py createsuperuser

# Start server
python manage.py runserver
````

---

## 📄 License

This project is licensed under the **MIT License**.

