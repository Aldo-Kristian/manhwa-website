# Sequence Diagram

## Manga / Manhwa / Manhua Reader & CMS

---

## 1. Overview

The Sequence Diagram describes how actors and system components communicate with each other over time to complete specific use cases.

The diagrams in this document focus on three important workflows:

1. Reader Login
2. Reader Reads a Chapter
3. Admin Publishes a Chapter

The main system components are:

- Reader
- Admin
- Frontend
- Admin Frontend
- Backend API
- Database

---

## 2. Reader Login

### 2.1 Description

This sequence describes how a Reader authenticates with the system.

### 2.2 Sequence Flow

```mermaid
sequenceDiagram

    actor Reader
    participant Frontend
    participant API as Backend API
    participant DB as Database

    Reader->>Frontend: Open Login Page
    Frontend-->>Reader: Display Login Form

    Reader->>Frontend: Enter Email and Password
    Frontend->>API: POST /login

    API->>DB: Find User by Email
    DB-->>API: Return User Data

    API->>API: Verify Password

    alt Credentials Valid
        API-->>Frontend: Authentication Success
        Frontend-->>Reader: Redirect to Reader Platform
    else Credentials Invalid
        API-->>Frontend: Authentication Failed
        Frontend-->>Reader: Display Login Error
    end
```

### 2.3 Main Flow

1. Reader opens the Login page.
2. Frontend displays the login form.
3. Reader enters their credentials.
4. Frontend sends the credentials to the Backend API.
5. Backend searches for the user in the database.
6. Backend verifies the provided password.
7. If the credentials are valid, authentication succeeds.
8. Frontend redirects the Reader to the Reader Platform.
9. If the credentials are invalid, an error is displayed.

---

## 3. Reader Reads a Chapter

### 3.1 Description

This sequence describes how a Reader opens a published chapter and retrieves its pages.

### 3.2 Sequence Flow

```mermaid
sequenceDiagram

    actor Reader
    participant Frontend
    participant API as Backend API
    participant DB as Database

    Reader->>Frontend: Open Chapter
    Frontend->>API: GET /chapters/{chapterId}

    API->>DB: Find Chapter
    DB-->>API: Return Chapter Data

    API->>API: Check Publication Status

    alt Chapter Published
        API->>DB: Get Chapter Pages
        DB-->>API: Return Ordered Pages

        API-->>Frontend: Chapter Data + Pages
        Frontend-->>Reader: Display Chapter

        loop Navigate Pages
            Reader->>Frontend: Open Next Page
            Frontend-->>Reader: Display Page
        end

        Reader->>Frontend: Finish / Leave Chapter
        Frontend->>API: Save Reading Progress
        API->>DB: Update Reading History
        DB-->>API: Progress Saved
        API-->>Frontend: Progress Saved

    else Chapter Not Published
        API-->>Frontend: Chapter Unavailable
        Frontend-->>Reader: Display Unavailable Message
    end
```

### 3.3 Main Flow

1. Reader selects a chapter.
2. Frontend requests the chapter from the Backend API.
3. Backend retrieves the chapter from the database.
4. Backend checks whether the chapter is published.
5. If the chapter is not published, access is rejected.
6. If the chapter is published, Backend retrieves its pages.
7. Database returns the pages in their defined order.
8. Backend sends the chapter data and pages to the Frontend.
9. Frontend displays the chapter.
10. Reader navigates through the chapter pages.
11. When the Reader finishes or leaves the chapter, the Frontend sends reading progress.
12. Backend stores or updates the Reader's reading history.

---

## 4. Admin Publishes a Chapter

### 4.1 Description

This sequence describes how an Admin creates and publishes a chapter through the Admin CMS.

### 4.2 Sequence Flow

```mermaid
sequenceDiagram

    actor Admin
    participant AdminFrontend as Admin Frontend
    participant API as Backend API
    participant DB as Database

    Admin->>AdminFrontend: Login
    AdminFrontend->>API: POST /admin/login

    API->>DB: Find Admin Account
    DB-->>API: Return Admin Data

    API->>API: Verify Credentials

    alt Credentials Valid
        API-->>AdminFrontend: Authentication Success
        AdminFrontend-->>Admin: Open Admin Dashboard
    else Credentials Invalid
        API-->>AdminFrontend: Authentication Failed
        AdminFrontend-->>Admin: Display Login Error
    end

    Admin->>AdminFrontend: Select Series
    AdminFrontend->>API: GET /series/{seriesId}
    API->>DB: Get Series
    DB-->>API: Return Series
    API-->>AdminFrontend: Display Series

    Admin->>AdminFrontend: Create Chapter
    AdminFrontend->>API: POST /chapters
    API->>DB: Create Chapter
    DB-->>API: Return Chapter
    API-->>AdminFrontend: Chapter Created

    Admin->>AdminFrontend: Upload Chapter Pages
    AdminFrontend->>API: POST /chapters/{chapterId}/pages
    API->>DB: Store Page Metadata
    DB-->>API: Pages Stored
    API-->>AdminFrontend: Upload Successful

    Admin->>AdminFrontend: Set Publication Date
    AdminFrontend->>API: Update Chapter
    API->>DB: Update Chapter Data
    DB-->>API: Update Successful
    API-->>AdminFrontend: Chapter Updated

    Admin->>AdminFrontend: Publish Chapter
    AdminFrontend->>API: PATCH /chapters/{chapterId}/publish

    API->>DB: Update Chapter Status
    DB-->>API: Status Updated

    API-->>AdminFrontend: Chapter Published
    AdminFrontend-->>Admin: Display Publication Success
```

### 4.3 Main Flow

1. Admin opens the Admin CMS.
2. Admin submits login credentials.
3. Backend authenticates the Admin.
4. Admin opens the dashboard.
5. Admin selects the target series.
6. Admin creates a new chapter.
7. Backend stores the chapter.
8. Admin uploads the chapter pages.
9. Backend stores the page metadata and ordering.
10. Admin sets the publication date.
11. Backend updates the chapter information.
12. Admin selects the publish action.
13. Backend updates the chapter publication status.
14. The chapter becomes available to Readers.

---

## 5. Component Interaction Summary

| Actor | Component | Responsibility |
|---|---|---|
| Reader | Frontend | Provides the Reader interface |
| Admin | Admin Frontend | Provides the CMS interface |
| Frontend | Backend API | Sends requests and receives system data |
| Admin Frontend | Backend API | Sends administrative requests |
| Backend API | Database | Reads and modifies persistent data |
| Database | Backend API | Returns requested data or confirms changes |

---

## 6. Sequence Diagram Summary

| Sequence | Primary Actor | Main Process |
|---|---|---|
| Reader Login | Reader | Authenticate user credentials |
| Reader Reads a Chapter | Reader | Retrieve and display a published chapter |
| Admin Publishes a Chapter | Admin | Create, configure, and publish a chapter |

---

## 7. Related Documentation

- [Software Requirements Specification](SRS.md)
- [Use Case Documentation](use-case.md)
- [Activity Diagram](activity-diagram.md)
- Database / ERD documentation
- System Architecture documentation

---

## 8. Completion Criteria

The Sequence Diagram documentation is considered complete when:

- Reader authentication flow is documented.
- Reader chapter-reading flow is documented.
- Admin chapter publication flow is documented.
- Actor-to-frontend communication is represented.
- Frontend-to-Backend communication is represented.
- Backend-to-Database communication is represented.
- Important success and failure conditions are represented.
- The documented sequences are consistent with the SRS, Use Case Diagram, and Activity Diagram.