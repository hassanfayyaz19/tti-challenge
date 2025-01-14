# Project Management API

A RESTful API built with Laravel for managing projects and tasks. This API provides endpoints for creating, reading, updating, and deleting projects and their associated tasks.

## Prerequisites

- PHP >= 8.2
- Composer
- MySQL >= 5.8
- Git

## Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/project-management-api.git
cd project-management-api
```

2. Install dependencies
```bash
composer install
```

3. Environment Setup
```bash
cp .env.example .env
php artisan key:generate
```

4. Configure your `.env` file with your database credentials:
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=project_management
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

5. Run migrations and seeders
```bash
php artisan migrate
php artisan db:seed
```

## Running the Application

Start the development server:
```bash
php artisan serve
```

The API will be available at `http://localhost:8000`

## API Documentation

### Projects

#### List all projects
- **GET** `/api/projects`
- **Response**: Array of projects
```json
{
    "data": [
        {
            "id": 1,
            "title": "Project Title",
            "description": "Project Description",
            "status": "open"
        }
    ]
}
```

#### Create a project
- **POST** `/api/projects`
- **Body**:
```json
{
    "title": "New Project",
    "description": "Project Description",
    "status": "open"
}
```
- **Required fields**: `title`

#### Get single project
- **GET** `/api/projects/{id}`
- **Response**: Project details with tasks

#### Update project
- **PUT** `/api/projects/{id}`
- **Body**: Same as create project

#### Delete project
- **DELETE** `/api/projects/{id}`

### Tasks

#### List project tasks
- **GET** `/api/projects/{project_id}/tasks`
- **Response**: Array of tasks

#### Create task
- **POST** `/api/projects/{project_id}/tasks`
- **Body**:
```json
{
    "title": "Task Title",
    "description": "Task Description",
    "assigned_to": "John Doe",
    "due_date": "2025-02-01",
    "status": "to_do"
}
```
- **Required fields**: `title`

#### Get single task
- **GET** `/api/tasks/{id}`

#### Update task
- **PUT** `/api/tasks/{id}`
- **Body**: Same as create task

#### Delete task
- **DELETE** `/api/tasks/{id}`

## Response Formats

### Success Response
```json
{
    "data": {
        // Resource data
    },
    "message": "Success message"
}
```

### Error Response
```json
{
    "error": {
        "message": "Error message",
        "details": {
            // Validation errors or additional details
        }
    }
}
```

## Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `404` - Not Found
- `422` - Validation Error
- `500` - Server Error

## Database Schema

### Projects Table
- `id` - Primary Key
- `title` - String
- `description` - Text (nullable)
- `status` - Enum ('open', 'in_progress', 'completed')
- `timestamps`

### Tasks Table
- `id` - Primary Key
- `project_id` - Foreign Key
- `title` - String
- `description` - Text (nullable)
- `assigned_to` - String (nullable)
- `due_date` - Date (nullable)
- `status` - Enum ('to_do', 'in_progress', 'done')
- `timestamps`

## **Decisions I Made**

1. Integrated the **Laravel Pint** package to ensure consistent code formatting. Additionally, set up Git pre-commit hooks to automatically format code during commits.
2. Adhered to **PSR-12 Standards** for coding style and structure to maintain readability and consistency.
3. Utilized **API Resource Controllers** to automatically generate and organize API routes efficiently.
4. Implemented **API Resources and Collections** to standardize and customize API responses as needed, allowing flexibility for future modifications.
5. Created dedicated **Request Classes** for API validation to keep the codebase clean and organized. These classes also support custom error messages for validation failures.
