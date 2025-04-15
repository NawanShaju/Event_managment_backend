# Event managment-backend

This is the backend component of the Event Management System, a web application that allows users to register, browse, create, RSVP to events, and more. It is built using Python Flask, SQLAlchemy, and PostgreSQL, with JWT-based authentication and role-based access control.

Features:

User registration & login (with JWT)
Role-based access (admin & regular users)
Event creation (admin only)
RSVP functionality for users
Email confirmation on RSVP
Secure password hashing (bcrypt)
RESTful API design
CORS enabled for frontend interaction
Tech Stack

Python 3.11+
Flask
SQLAlchemy
Flask-JWT-Extended
PostgreSQL
Flask-Mail
Flask-CORS

1. Clone the repository
git clone https://github.com/yourusername/event-management.git
cd event-management/backend

2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate 

3. Install dependencies
pip install -r requirements.txt

4. Create a .env file
Create a .env file in the backend directory with the following variables:
FLASK_APP=app
FLASK_ENV=development
SECRET_KEY=your-secret-key
JWT_SECRET_KEY=your-jwt-secret
DATABASE_URL=postgresql://username:password@localhost:5432/event_db
MAIL_SERVER=smtp.example.com
MAIL_PORT=587
MAIL_USE_TLS=True
MAIL_USERNAME=your-email@example.com
MAIL_PASSWORD=your-email-password
MAIL_DEFAULT_SENDER=your-email@example.com

5. Set up the database
Create the PostgreSQL database:
CREATE DATABASE event_db;

flask db upgrade

6. Run the development server
flask run

🧪 Running Tests

Navigate to the backend folder and run:
pytest

📁 Directory Structure

backend/
│
├── app/
│   ├── __init__.py        # App factory
│   ├── models.py          # SQLAlchemy models
│   ├── routes/            # Blueprint route modules
│   ├── utils.py           # Helper functions (e.g., email)
│   └── ...
│
├── tests/                 # Unit tests
│   ├── conftest.py
│   └── test_*.py
│
├── migrations/            # Flask-Migrate files
├── .env                   # Environment variables
├── requirements.txt
└── README.md

✍️ API Endpoints Overview

Method	Endpoint	          Description	        Auth Required  Role
POST	/api/auth/register	  Register a new user	❌	            -
POST	/api/auth/login	      Log in a user	        ❌	            -
GET	    /api/events/	      List all events	    ❌	            -
POST	/api/events/	      Create a new event	✅	            Admin
GET	    /api/events/<id>	  Get event details	    ❌	            -
POST	/api/events/<id>/rsvp RSVP to an event	    ✅	            User/Admin


Notes on Implementation

JWT tokens are stored on the client side and passed via the Authorization header as a Bearer token.
admin_required is a custom decorator that restricts access to certain endpoints based on user role.
RSVP functionality triggers a confirmation email using Flask-Mail.
CORS is handled using Flask-CORS, allowing requests from the frontend (localhost:3000 by default).

Future Improvements

Pagination for events
Admin dashboard with event analytics
Email verification on registration
Reminder emails before events