# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities
- Persistent relational database (SQLite via SQLAlchemy)

## Getting Started

1. Install the dependencies:

   ```
   pip install -r requirements.txt
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister from an activity                                     |

## Data Model

The application uses a relational SQLite database (via SQLAlchemy) for persistent storage:

1. **activities** table – one row per extracurricular activity:

   - `name` (primary key) – unique activity name
   - `description` – short description of the activity
   - `schedule` – meeting schedule
   - `max_participants` – maximum number of participants allowed

2. **participants** table – enrollment records (one row per student/activity pair):

   - `id` – auto-increment primary key
   - `activity_name` (foreign key → activities.name)
   - `email` – student email address

Data is stored in `mergington.db` (SQLite file, excluded from version control) and persists across server restarts. The database is seeded with default activities on first run.
