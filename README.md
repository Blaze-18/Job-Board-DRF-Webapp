
````markdown
# Djob

**Djob** is a modern job portal for job seekers and employers. It allows users to browse, post, and apply for jobs. The platform supports job search and filtering, user authentication, and provides a foundation for future enhancements such as a job recommendation engine.

---

## 🚀 Key Features

- **User Authentication:** Secure login and signup for job seekers and employers.
- **Job Posting & Editing:** Employers can post, edit, and delete jobs.
- **Search & Filters:** Search jobs by title, location, category, or other criteria.
- **Job Application Tracking:** Users can track applied jobs and employers can manage applicants.
- **API Integration:** Backend powered by Django REST Framework exposing RESTful APIs.
- **State Management:** Frontend state management using Pinia.

---

## 🛠️ Technology Stack

**Backend:** Django REST Framework, Python 3.x, SQLite  
**Frontend:** Nuxt3, TailwindCSS, TypeScript/JavaScript, Pinia for state management  

---

## 💻 Screenshots

- **Browse jobs**  
  ![Browse jobs](/Job-Board-DRF-Webapp/screenshots/Browse.png)  

- **Job card / details**  
  ![Job details](/Job-Board-DRF-Webapp/screenshots/Job.png)  

- **Dashboard**  
  ![Dashboard](/Job-Board-DRF-Webapp/screenshots/Dashboard.png)  

- **Signup / Login**  
  ![Signup page](/Job-Board-DRF-Webapp/screenshots/Signup.png)  


---

## 📹 Demo Video

<!-- Add demo video here when available -->

---

## ⚡ Installation

### Backend
```bash
cd djob_backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser  # Create admin user
python manage.py runserver
````

### Frontend

```bash
cd djob_frontend
npm install
npm run dev
```

---

## 📄 License

This project is licensed under the **MIT License**.

