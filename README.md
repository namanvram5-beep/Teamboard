# Teamboard
Teamboard for Airtribe


````md
# TeamBoard - B2B Knowledge Base API

## Overview

TeamBoard is a backend API platform that provides a searchable technical knowledge base for B2B customers. Companies can register, authenticate using JWT tokens, search knowledge base entries, and admins can view platform usage analytics.

This project was built using Django and Django REST Framework.

---

## Features

### Authentication
- Company registration
- Auto-generated API key using Django signals
- JWT login using SimpleJWT

### Knowledge Base Search
- Search by keyword across questions and answers
- Case-insensitive matching
- Query logging for every request

### Admin Dashboard
- Total queries made
- Active companies count
- Top searched terms

### Security
- JWT-protected endpoints by default
- Custom admin-only permission class

---

## Tech Stack

- Python
- Django
- Django REST Framework
- SimpleJWT
- SQLite (local development)
- PostgreSQL compatible
- python-dotenv

---

## Project Structure

```text
teamboard/
├── api/
├── teamboard/
├── manage.py
├── requirements.txt
├── README.md
├── .gitignore
````

---

## Installation & Setup

### 1. Clone Project

```bash
git clone <your-github-repo-url>
cd teamboard
```

### 2. Create Virtual Environment

```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Create .env File

Create `.env` in root folder:

```env
SECRET_KEY=your-secret-key
DEBUG=True
DB_NAME=teamboard
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=localhost
DB_PORT=5432
```

### 5. Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Run Server

```bash
python manage.py runserver
```

Server runs on:

```text
http://127.0.0.1:8000/
```

---

## Seed Knowledge Base Data

```bash
python manage.py shell
```

Then run:

```python
from api.models import KBEntry

KBEntry.objects.create(
    question="What is select_related in Django ORM?",
    answer="select_related performs SQL JOIN and fetches related objects.",
    category="database"
)
```

Repeat for additional entries.

---

## API Endpoints

### Register

**POST**

```text
/api/auth/register/
```

Body:

```json
{
  "username": "company1",
  "password": "securepass123",
  "company_name": "Company One",
  "email": "company1@test.com"
}
```

---

### Login

**POST**

```text
/api/auth/login/
```

---

### Query Knowledge Base

**POST**

```text
/api/kb/query/
```

Headers:

```text
Authorization: Bearer <JWT_TOKEN>
```

Body:

```json
{
  "search": "JWT"
}
```

---

### Admin Usage Summary

**GET**

```text
/api/admin/usage-summary/
```

Requires admin role token.

---

## Postman Collection

Import the provided Postman collection JSON and run all 11 required test scenarios.

---

## Notes

* SQLite used locally due environment limitations.
* Project is fully compatible with PostgreSQL using `.env` configuration.
* API keys are auto-generated via Django signals.



## Author

Naman Varma

