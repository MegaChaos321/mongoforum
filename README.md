# MongoForum

A lightweight, full-stack discussion forum application built with **Next.js** and **MongoDB**. This project was developed as an academic assignment for a **NoSQL Database** course to demonstrate document database modeling, relationship management, and server-side data operations.

## 📖 Overview

MongoForum is a simple, modern forum platform where users can register accounts, publish discussion topics, and participate in conversations through comments. It showcases basic CRUD operations, API routes, optimistic UI updates, and data integrity techniques such as manual cascade deletion using document references.

## ✨ Features

* **User Authentication:**
  * User registration and login using `bcryptjs` for secure password hashing.
  * Session handling using local storage state for client access control.

* **Topic Management:**
  * **Collapsible Creation Form:** Authenticated users can create new topics directly on the homepage via an interactive collapsible form.
  * View all topics on the homepage with dynamic pagination.
  * Topic deletion restricted strictly to the author.

* **Comment System:**
  * Add, edit, and delete comments on individual topic pages.
  * **Optimistic Updates ("Masking"):** Instant visual updates on comment edits/creations without needing a page refresh.
  * "Read More" functionality for expanding lengthy comments.

* **Backend Cascade Deletion:**
  * Service-level logic enforcing relational integrity across document collections:
    * **User Deletion:** Automatically purges all topics and comments authored by the user.
    * **Topic Deletion:** Automatically purges all associated comments.

## 🛠️ Tech Stack & Dependencies

* **Framework:** Next.js (JavaScript, App Router)
* **Database:** MongoDB
* **Database Driver:** `mongodb` (Native Node.js Driver)
* **Authentication / Security:** `bcryptjs`
* **Styling / UI:** Modern CSS / React components

## 🗂️ Data Structure

The application models data across three primary MongoDB collections:

1. **`users`**: Stores user credentials and basic account data.
2. **`topics`**: Stores forum posts linked to an `authorId`.
3. **`comments`**: Stores individual responses linked to both a `topicId` and an `authorId`.

## 🌐 Page Structure

The application consists of 4 main routes using the Next.js App Router:

| Route | Description |
| ----- | ----- |
| `/` | **Homepage:** Displays paginated list of forum topics and includes a collapsible form for authenticated users to create topics. |
| `/login` | **Login Page:** Authenticates existing users using hashed passwords. |
| `/registo` | **Register Page:** Account creation form. |
| `/topic/[id]` | **Topic Detail Page:** Displays single topic details, full comment thread, and creation/edit forms. |

## 🔌 API Endpoints

The Next.js App Router handles serverless API route handlers to expose the following endpoints:

| Endpoint | Method | Description |
| --- | --- | --- |
| `/api/registo` | `POST` | Register a new user account |
| `/api/login` | `POST` | Authenticate existing user |
| `/api/topicos` | `GET` | Fetch paginated list of topics |
| `/api/topicos` | `POST` | Create a new topic (Auth required) |
| `/api/topicos/[id]` | `GET` | Fetch topic details by ID |
| `/api/topicos/[id]` | `DELETE` | Delete topic and trigger cascade deletion of associated comments |
| `/api/topicos/[id]/comentarios` | `GET` | Fetch all comments belonging to a specific topic |
| `/api/comentarios` | `POST` | Create a new comment |
| `/api/comentarios/[id]` | `PUT` | Edit an existing comment |
| `/api/comentarios/[id]` | `DELETE` | Delete an existing comment |

## 🚀 Getting Started

Follow these steps to set up and run the project locally.

### Prerequisites

* [Node.js](https://nodejs.org/) (v18 or higher recommended)
* A running [MongoDB](https://www.mongodb.com/) database instance (local or via MongoDB Atlas)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/MegaChaos321/mongoforum.git
   cd mongoforum
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up Environment Variables:**
   Create a `.env.local` file in the root directory and add your MongoDB connection string:
   ```env
   MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/mongoforum?retryWrites=true&w=majority
   ```

4. **Run the development server:**
   ```bash
   npm run dev
   ```

5. **Access the application:**
   Open [http://localhost:3000](http://localhost:3000) in your browser.

## 🎓 Academic Context

This repository was created as a course assignment for a **NoSQL Databases** module. Key learning objectives included:

* Modeling relationships in document-oriented databases.
* Implementing business logic for data integrity without traditional RDBMS constraints.
* Integrating MongoDB with modern full-stack web frameworks like Next.js.
