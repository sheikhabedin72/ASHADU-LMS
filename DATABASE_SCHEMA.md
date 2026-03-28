# Database Schema Design for ASHADU-LMS

## 1. Users Table
- **users**: This table stores all registered users. It utilizes role-based access control to manage user permissions.
    - **id** (INT, Primary Key): A unique identifier for each user.
    - **username** (VARCHAR): The unique username of the user.
    - **password_hash** (VARCHAR): Hashed password for authentication.
    - **email** (VARCHAR): User's email, unique to each user.
    - **role** (ENUM): Defines user roles (e.g., 'Student', 'Instructor', 'Admin').
    - **created_at** (TIMESTAMP): The timestamp of user registration.

### Relationships:
- Each user can have multiple courses through the enrollments table.

---

## 2. Courses Table
- **courses**: Contains information about the courses offered in the LMS.
    - **id** (INT, Primary Key): A unique identifier for the course.
    - **title** (VARCHAR): The title of the course.
    - **description** (TEXT): A detailed description of what the course entails.
    - **metadata** (JSON): AI-generated metadata about the course, including keywords for optimizing the content based on user needs.
    - **created_by** (INT, Foreign Key): Refers to the user id of the instructor who created the course.
    - **created_at** (TIMESTAMP): The timestamp when the course was created.

### Relationships:
- Each course can have multiple lessons associated with it.

---

## 3. Lessons Table
- **lessons**: This table contains lessons associated with each course.
    - **id** (INT, Primary Key): Unique identifier for each lesson.
    - **course_id** (INT, Foreign Key): The ID of the course to which the lesson belongs.
    - **title** (VARCHAR): Title of the lesson.
    - **content** (TEXT): The main content of the lesson.
    - **order** (INT): Order of the lesson within a course.

### Relationships:
- Lessons belong to a specific course.

---

## 4. Quizzes Table
- **quizzes**: Holds information about quizzes assigned to lessons.
    - **id** (INT, Primary Key): Unique identifier for each quiz.
    - **lesson_id** (INT, Foreign Key): Refers to the lesson the quiz is part of.
    - **title** (VARCHAR): Title of the quiz.
    - **questions** (TEXT): Serialized or JSON string representing the questions for the quiz.
    - **created_at** (TIMESTAMP): Timestamp of when the quiz was created.

### Relationships:
- Quizzes are linked to specific lessons.

---

## 5. Student Progress Table
- **student_progress**: Tracks the progress of students in each course.
    - **id** (INT, Primary Key): Unique identifier for each progress record.
    - **user_id** (INT, Foreign Key): ID of the student.
    - **course_id** (INT, Foreign Key): ID of the course being tracked.
    - **completed_lessons** (INT): The number of lessons completed by the student.
    - **score** (FLOAT): The latest score achieved by the student in quizzes.
    - **enrollment_date** (TIMESTAMP): Date when the student enrolled in the course.

### Relationships:
- Links users with their respective courses and tracks progress.

---

## 6. Enrollments Table
- **enrollments**: Keeps track of student enrollments in courses.
    - **id** (INT, Primary Key): Unique identifier for each enrollment.
    - **user_id** (INT, Foreign Key): The ID of the user enrolled in the course.
    - **course_id** (INT, Foreign Key): The ID of the course the user is enrolled in.
    - **Enrollment_date** (TIMESTAMP): Date of enrollment.

### Relationships:
- Connects users to courses they have enrolled in, serving as a bridge table between users and courses.

---

## Conclusion
This schema is designed to support a robust LMS structure, with considerations for role-based access and necessary relationships between core entities. Each table is built to facilitate efficient data management and querying for both reporting and operational purposes.

