# Student Management System

A modern Vue.js application for managing student records with a clean, responsive interface.

## Features

- Display student records in a responsive table
- Add new students with a modal form
- Search and filter student records
- Sort data by different fields
- Delete student records with confirmation
- Pagination for handling large datasets

## Technologies Used

- Vue.js 3
- Bootstrap 5
- Bootstrap Icons
- JSON Server for mock API

## Project Setup

```bash
# Install dependencies
npm install

# Start the mock API server (port 3001)
npx json-server --watch db.json --port 3001

# Run the development server
npm run serve
```

## API Structure

The application uses a REST API with the following endpoints:

- `GET /students` - Retrieve all students
- `POST /students` - Add a new student
- `DELETE /students/:id` - Delete a student

## Screenshots

- Dashboard view with student records
- Responsive design for mobile and desktop
- Search and filtering functionality

## Development

This project was created as part of a lab assignment to demonstrate CRUD operations with Vue.js.

## Author

Ehab
