# Cardb Vue Fullstack

Fullstack project built as a lab exercise: a simple Car database with a
Vue.js frontend and a Spring Boot + MySQL backend.

The goal is to show how both parts are connected and how to run the project
locally.

⸻

## Project structure

.
├── backend/     # Spring Boot + MySQL API (Java)
└── frontend/    # Vue 3 SPA (Vite)
	•	Backend: /backend (Java 17, Spring Boot, Spring Data JPA, MySQL)
	•	Frontend: /frontend (Vue 3, Vite, Pinia, Axios, Vue Router)

The frontend consumes the REST API exposed by the backend.

⸻

## Backend (Spring Boot)

Path: backend/

Main entry point:
	•	src/main/java/com/ironhack/cardb/CardbApplication.java

Main REST controller:
	•	src/main/java/com/ironhack/cardb/controller/CarController.java
Base path: /api/cars

Database

The application uses MySQL. Configuration is in:
	•	backend/src/main/resources/application.properties

Default settings:

spring.datasource.url=jdbc:mysql://localhost:3307/cardb?useSSL=false&createDatabaseIfNotExist=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

The database cardb will be created automatically if it does not exist.

Run the backend

From the root of the project:

cd backend
./mvnw spring-boot:run

or (if Maven is installed globally):

cd backend
mvn spring-boot:run

The API will be available at:

http://localhost:8080/api/cars

⸻

## Frontend (Vue 3)

Path: frontend/

Key files:
	•	src/services/api.js → Axios instance pointing to the backend
	•	src/stores/carStore.js → State management for cars
	•	src/pages/Home.vue, Detail.vue, CreateEdit.vue → Main views
	•	src/router/index.js → Vue Router configuration

The frontend reads the API URL from the environment variable VITE_API_URL.
If it is not defined, it falls back to http://localhost:8080/api.

Environment variable (optional)

Create a .env file in frontend/ if you want to be explicit:

VITE_API_URL=http://localhost:8080/api

Run the frontend

From the root of the project:

cd frontend
npm install
npm run dev

By default Vite will start on:

http://localhost:5173/

Make sure the backend is running first, so the app can load and manage cars
through the REST API.

⸻

## How frontend and backend are linked
	•	The backend exposes REST endpoints under /api/cars (GET, POST, PUT, DELETE).
	•	The frontend uses axios with baseURL = VITE_API_URL
(or http://localhost:8080/api by default).
	•	All car operations in the UI (list, details, create, edit, delete) are
performed through these HTTP calls.

⸻

## Notes for evaluation
	•	This repository contains both:
	•	backend/ → Spring Boot + MySQL API (cardb)
	•	frontend/ → Vue 3 SPA (car-vue)
	•	To test the project:
	1.	Start MySQL on localhost:3307 with user root / password root.
	2.	Run the backend (backend).
	3.	Run the frontend (frontend).
	4.	Open the browser at `http://localhost:5173/