````markdown
# Software Requirements Specification (SRS)

## Manga / Manhwa / Manhua Reader & CMS

---

# 1. Introduction

## 1.1 Purpose

This document defines the software requirements for the **Manga / Manhwa / Manhua Reader & CMS** web application.

The purpose of this document is to describe:

- System functionality
- User roles
- Functional requirements
- Non-functional requirements
- System constraints
- External interfaces
- Data requirements
- Business rules
- Future development considerations

This document will serve as a technical reference during the design, development, testing, and deployment phases of the project.

---

## 1.2 Project Scope

The system is a web-based platform for discovering and reading:

- Manga
- Manhwa
- Manhua

The system consists of two primary components:

1. **Reader Platform**
2. **Admin CMS**

### Reader Platform

The Reader Platform allows users to:

- Register and log in
- Log out
- Browse series
- Search for series
- Filter series
- View series details
- View chapter lists
- Read chapters
- Navigate between chapter pages
- Navigate to previous and next chapters
- Bookmark series
- View bookmarked series
- Track reading history
- Continue reading from previous reading progress
- Comment on chapters
- Discover recently added series
- Discover recently updated series
- Discover latest chapters

### Admin CMS

The Admin CMS allows administrators to:

- Log in
- Log out
- View dashboard statistics
- Manage series
- Manage series covers
- Manage content types
- Manage genres
- Manage chapters
- Upload chapter pages
- Manage chapter page order
- Publish and unpublish chapters
- Set chapter publication dates
- Manage users
- Moderate comments

---

## 1.3 Supported Content Types

The system supports three content types:

- Manga
- Manhwa
- Manhua

The system uses a generic `Series` concept rather than creating separate entities for each content type.

Conceptually:

```text
Series
├── Manga
├── Manhwa
└── Manhua
````

This approach allows the system to support different types of comics without requiring separate database structures for each type.

---

# 2. Overall Description

## 2.1 Product Perspective

The application is a web-based content management and reading platform.

The system can be divided into the following major components:

```text
                    Web Application
                          |
          +---------------+---------------+
          |                               |
   Reader Platform                    Admin CMS
          |                               |
    +-----+-----+                 +-------+-------+
    |     |     |                 |       |       |
 Browse Search Read            Series  Chapter  User
    |     |     |                 |       |       |
 Bookmark History Comment       Genre   Pages   Moderation
```

The Reader Platform is intended for normal users, while the Admin CMS is intended for authorized administrators.

---

## 2.2 User Classes

The system contains two primary user classes:

### 2.2.1 Reader

A Reader is a registered user who can access reading and personalization features.

Reader capabilities include:

* Authentication
* Browsing
* Searching
* Filtering
* Reading
* Bookmarking
* Reading history
* Comments

### 2.2.2 Administrator

An Administrator manages the content and users of the platform through the Admin CMS.

Administrator capabilities include:

* Content management
* Chapter management
* Page management
* Genre management
* User management
* Comment moderation
* Basic dashboard monitoring

---

## 2.3 Operating Environment

The application is designed as a web application.

### Client Environment

The Reader Platform should support modern web browsers, including:

* Google Chrome
* Mozilla Firefox
* Microsoft Edge
* Safari

### Server Environment

The application requires:

* Web server
* Application backend
* Database server
* File or object storage for chapter images

The exact technologies may be determined during the architecture and implementation phases.

---

## 2.4 Product Functions

The major system functions are:

```text
Authentication
    |
    +-- Register
    +-- Login
    +-- Logout

Content Discovery
    |
    +-- Browse Series
    +-- Search
    +-- Filter
    +-- Recently Added
    +-- Recently Updated
    +-- Latest Chapters

Series
    |
    +-- Series Detail
    +-- Chapter List
    +-- Genres
    +-- Content Type

Reading
    |
    +-- Read Chapter
    +-- Page Navigation
    +-- Previous Chapter
    +-- Next Chapter
    +-- Reading Progress

User Features
    |
    +-- Bookmark
    +-- Reading History
    +-- Comments

Admin CMS
    |
    +-- Dashboard
    +-- Series Management
    +-- Chapter Management
    +-- Page Management
    +-- Genre Management
    +-- User Management
    +-- Comment Moderation
```

---

# 3. Functional Requirements

## 3.1 Authentication Requirements

### FR-AUTH-01 — User Registration

The system shall allow visitors to create an account.

The registration process shall require appropriate account information such as:

* Username
* Email
* Password

The system shall validate the submitted information before creating the account.

---

### FR-AUTH-02 — User Login

The system shall allow registered users to authenticate using their account credentials.

---

### FR-AUTH-03 — User Logout

The system shall allow authenticated users to log out of the system.

---

### FR-AUTH-04 — Authentication Protection

The system shall restrict authenticated-only features to logged-in users.

Examples:

* Bookmark
* Reading history
* Commenting
* User account features

---

## 3.2 Content Discovery Requirements

### FR-DISC-01 — Browse Series

The system shall allow users to browse available series.

---

### FR-DISC-02 — Browse by Content Type

The system shall allow users to filter or browse series by:

* Manga
* Manhwa
* Manhua

---

### FR-DISC-03 — Browse by Genre

The system shall allow users to browse series based on genre.

---

### FR-DISC-04 — Search Series

The system shall provide a search function for finding series.

Search may use information such as:

* Series title
* Alternative title

---

### FR-DISC-05 — Series Detail

The system shall provide a detail page for each series.

The series detail page shall display information such as:

* Title
* Cover
* Description
* Content type
* Genres
* Chapter list
* Latest chapter
* Update information

---

## 3.3 Latest and Recent Content Requirements

The homepage shall provide content discovery sections focused on newly added and recently updated content.

### FR-DISC-06 — Recently Added Series

The system shall provide a section displaying recently added series.

The ordering shall be based on the series creation date.

Example:

```text
Newest Series
1. Series A
2. Series B
3. Series C
```

---

### FR-DISC-07 — Recently Updated Series

The system shall provide a section displaying series that have recently received chapter updates.

The ordering shall be based on the publication time of the latest published chapter.

Example:

```text
Series A
 └── Latest Chapter: Chapter 50
     Published: Today

Series B
 └── Latest Chapter: Chapter 120
     Published: Yesterday
```

An older series may therefore appear near the top when it receives a new chapter.

---

### FR-DISC-08 — Latest Chapters

The system shall provide a list of recently published chapters.

Each item may display:

* Series title
* Chapter number
* Chapter title
* Publication date
* Series cover

---

### FR-DISC-09 — Latest Updates

The system may provide a combined update feed containing recently updated series and chapters.

---

## 3.4 Series Requirements

### FR-SERIES-01 — View Series

Users shall be able to view the details of a series.

---

### FR-SERIES-02 — View Chapter List

Users shall be able to view the available chapters of a series.

---

### FR-SERIES-03 — Chapter Ordering

Chapters shall be displayed in a consistent order.

The system may provide:

* Ascending order
* Descending order

---

### FR-SERIES-04 — Series Content Type

Each series shall have one content type:

* Manga
* Manhwa
* Manhua

---

### FR-SERIES-05 — Series Genres

A series may contain one or more genres.

---

## 3.5 Chapter Requirements

### FR-CHAPTER-01 — View Chapter

Users shall be able to open an available chapter.

---

### FR-CHAPTER-02 — Chapter Availability

Only published chapters shall be available to normal readers.

Unpublished chapters shall not be publicly accessible through the Reader Platform.

---

### FR-CHAPTER-03 — Previous Chapter

The reader shall provide navigation to the previous chapter when available.

---

### FR-CHAPTER-04 — Next Chapter

The reader shall provide navigation to the next chapter when available.

---

### FR-CHAPTER-05 — Chapter Publication Date

Each chapter shall store a publication date or publication timestamp.

---

## 3.6 Chapter Page Requirements

### FR-PAGE-01 — Chapter Pages

Each chapter may contain multiple image pages.

Example:

```text
Chapter 1
├── Page 1
├── Page 2
├── Page 3
└── Page 4
```

---

### FR-PAGE-02 — Page Ordering

The system shall preserve the order of chapter pages.

---

### FR-PAGE-03 — Page Navigation

The reader shall allow users to navigate through chapter pages.

The exact reading mode may be determined during UI design.

Possible reading modes include:

* Vertical scrolling
* Individual page navigation

---

## 3.7 Reading Requirements

### FR-READ-01 — Read Chapter

Authenticated and unauthenticated users may read publicly available chapters according to the system's access rules.

---

### FR-READ-02 — Reading Progress

For authenticated users, the system shall be able to store reading progress.

The progress may include:

* Series
* Chapter
* Page
* Last reading timestamp

---

### FR-READ-03 — Continue Reading

The system shall allow authenticated users to continue reading from previously recorded reading progress.

---

## 3.8 Bookmark Requirements

### FR-BOOKMARK-01 — Add Bookmark

Authenticated users shall be able to bookmark a series.

---

### FR-BOOKMARK-02 — Remove Bookmark

Authenticated users shall be able to remove a series from their bookmarks.

---

### FR-BOOKMARK-03 — View Bookmarks

Authenticated users shall be able to view their bookmarked series.

---

## 3.9 Reading History Requirements

### FR-HISTORY-01 — Store Reading History

The system shall store reading activity for authenticated users.

---

### FR-HISTORY-02 — View Reading History

Authenticated users shall be able to view their reading history.

---

### FR-HISTORY-03 — Continue From History

Users shall be able to open a previously read chapter from their reading history.

---

## 3.10 Comment Requirements

### FR-COMMENT-01 — Chapter Comments

Users shall be able to comment on a specific chapter.

Comments shall be associated with the chapter rather than only the series.

---

### FR-COMMENT-02 — Create Comment

Authenticated users shall be able to submit comments.

---

### FR-COMMENT-03 — View Comments

Users shall be able to view comments associated with a chapter.

---

### FR-COMMENT-04 — Delete Comment

The system shall allow authorized administrators to delete inappropriate comments.

---

## 3.11 Admin Authentication Requirements

### FR-ADMIN-AUTH-01 — Admin Login

Administrators shall authenticate before accessing the Admin CMS.

---

### FR-ADMIN-AUTH-02 — Admin Logout

Administrators shall be able to log out.

---

### FR-ADMIN-AUTH-03 — Admin Access Control

Only authorized administrator accounts shall be able to access administrative functions.

---

# 4. Admin CMS Requirements

## 4.1 Dashboard

### FR-CMS-01 — Dashboard

The Admin CMS shall provide a dashboard containing basic system information.

Possible statistics include:

* Total series
* Total chapters
* Total users
* Total comments
* Recently added series
* Recently published chapters

---

## 4.2 Series Management

### FR-CMS-SERIES-01 — Create Series

Administrators shall be able to create a new series.

Series information may include:

* Title
* Alternative title
* Description
* Cover
* Content type
* Genres
* Status

---

### FR-CMS-SERIES-02 — View Series

Administrators shall be able to view existing series.

---

### FR-CMS-SERIES-03 — Update Series

Administrators shall be able to update series information.

---

### FR-CMS-SERIES-04 — Delete Series

Administrators shall be able to delete a series according to the system's data integrity rules.

---

### FR-CMS-SERIES-05 — Manage Series Cover

Administrators shall be able to upload or replace a series cover.

---

## 4.3 Content Type Management

The system shall associate every series with one supported content type:

* Manga
* Manhwa
* Manhua

Content types may initially be implemented as predefined system values.

---

## 4.4 Genre Management

### FR-CMS-GENRE-01 — Create Genre

Administrators shall be able to create genres.

---

### FR-CMS-GENRE-02 — Update Genre

Administrators shall be able to update genres.

---

### FR-CMS-GENRE-03 — Delete Genre

Administrators shall be able to delete genres when they are not required by existing data or according to defined database rules.

---

### FR-CMS-GENRE-04 — Assign Genre

Administrators shall be able to assign one or more genres to a series.

---

## 4.5 Chapter Management

### FR-CMS-CHAPTER-01 — Create Chapter

Administrators shall be able to create a chapter for a series.

Chapter information may include:

* Chapter number
* Chapter title
* Publication date
* Publication status

---

### FR-CMS-CHAPTER-02 — Update Chapter

Administrators shall be able to update chapter information.

---

### FR-CMS-CHAPTER-03 — Delete Chapter

Administrators shall be able to delete chapters according to system data integrity rules.

---

### FR-CMS-CHAPTER-04 — Publish Chapter

Administrators shall be able to publish a chapter.

---

### FR-CMS-CHAPTER-05 — Unpublish Chapter

Administrators shall be able to unpublish a chapter.

---

### FR-CMS-CHAPTER-06 — Set Publication Date

Administrators shall be able to set the publication date or timestamp of a chapter.

---

## 4.6 Chapter Page Management

### FR-CMS-PAGE-01 — Upload Pages

Administrators shall be able to upload image pages for a chapter.

---

### FR-CMS-PAGE-02 — Manage Page Order

Administrators shall be able to determine the order of pages within a chapter.

Example:

```text
Page 1
Page 2
Page 3
Page 4
```

---

### FR-CMS-PAGE-03 — Replace Page

Administrators may replace an existing chapter page.

---

### FR-CMS-PAGE-04 — Delete Page

Administrators may delete an existing chapter page.

---

## 4.7 User Management

### FR-CMS-USER-01 — View Users

Administrators shall be able to view registered users.

---

### FR-CMS-USER-02 — View User Details

Administrators shall be able to view relevant user information.

---

### FR-CMS-USER-03 — Manage User Status

Administrators may manage the status of user accounts according to the system's moderation rules.

---

## 4.8 Comment Moderation

### FR-CMS-COMMENT-01 — View Comments

Administrators shall be able to view user comments.

---

### FR-CMS-COMMENT-02 — View Comments by Chapter

Administrators shall be able to identify which chapter a comment belongs to.

---

### FR-CMS-COMMENT-03 — Delete Comment

Administrators shall be able to delete inappropriate or unwanted comments.

---

# 5. Non-Functional Requirements

## 5.1 Performance

### NFR-PERF-01

The application should provide reasonable response times for common operations.

Common operations include:

* Browsing series
* Searching
* Loading series details
* Loading chapter lists
* Loading chapter pages

---

### NFR-PERF-02

Chapter images should be delivered efficiently to reduce unnecessary loading time.

---

## 5.2 Security

### NFR-SEC-01

Passwords shall not be stored as plain text.

---

### NFR-SEC-02

Authentication credentials shall be handled securely.

---

### NFR-SEC-03

Admin functionality shall be protected by authorization controls.

---

### NFR-SEC-04

The system shall validate user input.

---

### NFR-SEC-05

The system shall protect against common web application vulnerabilities where applicable.

Examples include:

* SQL Injection
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Unauthorized access

---

## 5.3 Usability

### NFR-USE-01

The Reader Platform shall provide a simple and understandable navigation structure.

---

### NFR-USE-02

Users shall be able to access major functions without unnecessary navigation complexity.

---

### NFR-USE-03

The reading interface shall prioritize readability and convenient chapter navigation.

---

## 5.4 Reliability

### NFR-REL-01

The system should maintain data consistency when creating, updating, or deleting content.

---

### NFR-REL-02

The system should handle invalid requests without causing application failure.

---

## 5.5 Maintainability

### NFR-MAIN-01

The application shall use a modular structure to make future development easier.

---

### NFR-MAIN-02

The system shall maintain clear separation between major application components where applicable.

Examples:

```text
Frontend
Backend
Database
Storage
```

---

## 5.6 Scalability

### NFR-SCALE-01

The system architecture should allow the number of series, chapters, users, and chapter pages to increase without requiring a complete redesign.

---

## 5.7 Compatibility

### NFR-COMP-01

The application should support modern desktop and mobile web browsers.

---

### NFR-COMP-02

The Reader Platform should provide a responsive interface for different screen sizes.

---

# 6. External Interface Requirements

## 6.1 User Interface

The Reader Platform shall contain interfaces for:

* Home
* Browse
* Search
* Series detail
* Chapter list
* Reader
* Bookmarks
* Reading history
* Login
* Registration

---

## 6.2 Admin Interface

The Admin CMS shall contain interfaces for:

* Admin login
* Dashboard
* Series management
* Genre management
* Chapter management
* Chapter page management
* User management
* Comment moderation

---

## 6.3 Application Interface

The frontend shall communicate with the backend through an application interface such as an HTTP-based API.

The exact API architecture may be determined during the system architecture phase.

---

## 6.4 Database Interface

The backend shall communicate with a relational or suitable database system for storing structured application data.

---

## 6.5 File and Media Interface

Chapter pages and series covers require media storage.

The storage system shall support:

* Uploading images
* Retrieving images
* Replacing images
* Deleting images
* Maintaining relationships between stored images and application data

The exact storage technology will be determined during the architecture phase.

---

# 7. Data Requirements

The initial system shall contain the following major data entities.

## 7.1 User

Stores user account information.

Possible attributes:

```text
User
├── id
├── username
├── email
├── password
├── role
├── status
├── created_at
└── updated_at
```

---

## 7.2 Series

Stores information about manga, manhwa, and manhua.

Possible attributes:

```text
Series
├── id
├── title
├── alternative_title
├── description
├── cover
├── content_type
├── status
├── created_at
└── updated_at
```

---

## 7.3 Genre

Stores available genres.

Possible attributes:

```text
Genre
├── id
├── name
├── created_at
└── updated_at
```

---

## 7.4 Chapter

Stores chapters belonging to a series.

Possible attributes:

```text
Chapter
├── id
├── series_id
├── chapter_number
├── title
├── published_at
├── status
├── created_at
└── updated_at
```

---

## 7.5 Chapter Page

Stores information about individual pages of a chapter.

Possible attributes:

```text
ChapterPage
├── id
├── chapter_id
├── page_number
├── image_url
├── created_at
└── updated_at
```

---

## 7.6 Bookmark

Stores series bookmarked by users.

Possible attributes:

```text
Bookmark
├── id
├── user_id
├── series_id
└── created_at
```

---

## 7.7 Reading History

Stores user reading progress.

Possible attributes:

```text
ReadingHistory
├── id
├── user_id
├── series_id
├── chapter_id
├── page_number
├── last_read_at
└── updated_at
```

---

## 7.8 Comment

Stores comments made by users on chapters.

Possible attributes:

```text
Comment
├── id
├── user_id
├── chapter_id
├── content
├── created_at
└── updated_at
```

---

# 8. Business Rules

## BR-01 — Content Type

Every series shall have one supported content type:

```text
Manga
Manhwa
Manhua
```

---

## BR-02 — Chapter Ownership

Every chapter shall belong to exactly one series.

---

## BR-03 — Page Ownership

Every chapter page shall belong to exactly one chapter.

---

## BR-04 — Comment Ownership

Every comment shall belong to:

* One user
* One chapter

---

## BR-05 — Bookmark Ownership

A bookmark shall associate:

* One user
* One series

A user should not create duplicate bookmarks for the same series.

---

## BR-06 — Published Chapter

Only published chapters shall appear publicly in the Reader Platform.

---

## BR-07 — Recently Updated Series

A series shall be considered recently updated when it has a newly published chapter.

The ordering shall use the publication timestamp of the latest published chapter.

---

## BR-08 — Recently Added Series

Recently added series shall be ordered using the series creation timestamp.

---

# 9. Content Ordering Logic

## 9.1 Recently Added

The system shall sort newly created series by:

```text
series.created_at DESC
```

Conceptually:

```text
Newest Series
        ↓
Most recently created
        ↓
Oldest created
```

---

## 9.2 Recently Updated

The system shall determine the latest published chapter for each series.

Conceptually:

```text
Series A
└── Chapter 50
    published_at = 2026-09-27

Series B
└── Chapter 20
    published_at = 2026-09-25

Series C
└── Chapter 100
    published_at = 2026-09-20
```

The ordering becomes:

```text
Series A
Series B
Series C
```

The chapter number itself does not determine the update position.

The publication timestamp determines the update position.

---

## 9.3 Latest Chapters

Latest chapters shall be ordered using:

```text
chapter.published_at DESC
```

Only published chapters shall be included.

---

# 10. MVP Requirements

The initial Minimum Viable Product shall include the following features.

## Reader Platform

* User registration
* User login
* User logout
* Browse series
* Search series
* Filter by content type
* Filter by genre
* Series detail
* Chapter list
* Chapter reader
* Previous/next chapter navigation
* Bookmark
* Reading history
* Continue reading
* Chapter comments
* Recently added series
* Recently updated series
* Latest chapters

## Admin CMS

* Admin authentication
* Dashboard
* Series CRUD
* Series cover management
* Genre CRUD
* Chapter CRUD
* Chapter page upload
* Chapter page ordering
* Publish/unpublish chapter
* Publication date management
* User management
* Comment moderation

---

# 11. Project Boundaries

The MVP focuses on the core functionality required to build a functional comic reading platform and content management system.

The project prioritizes:

1. Content management
2. Content discovery
3. Chapter reading
4. User personalization
5. Basic community interaction
6. Administrative moderation

The project does not initially prioritize advanced social, commercial, or recommendation features.

---

# 12. Features Outside MVP

The following features are outside the initial MVP scope:

* Payment system
* Subscription system
* Premium content
* AI recommendation system
* Real-time chat
* Native mobile application
* Advanced social networking
* Complex notification system
* Advanced analytics
* Advertising management platform

These features may be considered in future development.

---

# 13. Future Development

Possible future improvements include:

## 13.1 Rating System

Users may be able to rate series.

---

## 13.2 Advanced Search

Future search functionality may support:

* Multiple genres
* Multiple content types
* Status
* Author
* Artist
* Release year
* Advanced sorting

---

## 13.3 Multiple Languages

The system may support multiple interface or content languages.

---

## 13.4 User Profiles

Users may receive public or private profile pages.

---

## 13.5 Followed Series

Users may follow series instead of only bookmarking them.

---

## 13.6 Notifications

Users may receive notifications when followed series receive new chapters.

---

## 13.7 Advanced Moderation

Future moderation features may include:

* Report system
* Moderation history
* Comment status
* User warnings
* Automated moderation assistance

---

## 13.8 Recommendation System

A recommendation system may be introduced in a future version.

Potential inputs may include:

* Reading history
* Bookmarks
* Genres
* Content types
* User interactions

This is not part of the MVP.

---

## 13.9 Mobile Application

A native Android or iOS application may be developed in the future.

---

# 14. System Constraints

The system may have the following constraints:

* Chapter pages require significant storage capacity.
* Image delivery may affect application performance.
* Large numbers of chapters may increase database size.
* Authentication must be implemented securely.
* Admin functionality must be protected from unauthorized access.
* The application depends on external infrastructure such as database and media storage.
* The final technology stack has not yet been fully determined.

---

# 15. Assumptions

The system is developed under the following assumptions:

1. Users have access to a modern web browser.
2. Users have an internet connection.
3. Administrators are authorized to manage platform content.
4. Administrators are responsible for uploading valid chapter content.
5. Chapter images are provided in supported formats.
6. The system has sufficient database and media storage.
7. The application backend is available when users access dynamic features.
8. The exact deployment infrastructure may change during development.

---

# 16. Project Development Dependencies

The system development may require:

* Frontend framework
* Backend framework
* Database
* Media storage
* Authentication mechanism
* API layer
* Version control
* Deployment environment

The exact technologies will be documented separately in the system architecture documentation.

---

# 17. Requirements Traceability

The major project requirements can be traced to the following system areas:

| Requirement Area    | Reader Platform | Admin CMS          |
| ------------------- | --------------- | ------------------ |
| Authentication      | Yes             | Yes                |
| Series browsing     | Yes             | Yes                |
| Search              | Yes             | Optional           |
| Filtering           | Yes             | Yes                |
| Series management   | No              | Yes                |
| Chapter reading     | Yes             | Preview/Management |
| Chapter management  | No              | Yes                |
| Page management     | No              | Yes                |
| Bookmark            | Yes             | No                 |
| Reading history     | Yes             | No                 |
| Comments            | Yes             | Yes                |
| User management     | No              | Yes                |
| Genre management    | No              | Yes                |
| Content publication | No              | Yes                |
| Recently added      | Yes             | Yes                |
| Recently updated    | Yes             | Yes                |

---

# 18. Requirements Completion Criteria

The requirements defined in this document shall be considered implemented when:

### Reader Platform

* Users can create and access accounts.
* Users can browse available series.
* Users can search and filter content.
* Users can view series details.
* Users can view chapter lists.
* Users can read published chapters.
* Users can navigate between chapters.
* Users can bookmark series.
* Users can view reading history.
* Users can continue reading.
* Users can comment on chapters.
* Users can discover recently added content.
* Users can discover recently updated content.
* Users can view latest chapters.

### Admin CMS

* Administrators can authenticate.
* Administrators can manage series.
* Administrators can manage genres.
* Administrators can manage chapters.
* Administrators can upload chapter pages.
* Administrators can manage page order.
* Administrators can publish and unpublish chapters.
* Administrators can manage users.
* Administrators can moderate comments.
* Administrators can view basic dashboard statistics.

---

# 19. Related Documentation

The following project documentation will be developed separately:

```text
docs/
├── SRS.md
├── use-case.md
├── activity-diagram.md
├── sequence-diagram.md
├── database.md
└── architecture.md
```

### SRS

Defines the functional and non-functional requirements of the system.

### Use Case Diagram

Describes interactions between actors and system functions.

### Activity Diagram

Describes workflows and business processes.

### Sequence Diagram

Describes interactions between system components over time.

### Database Documentation

Describes entities, attributes, relationships, and database structure.

### Architecture Documentation

Describes the technical architecture and communication between system components.

---

# 20. SRS Summary

The **Manga / Manhwa / Manhua Reader & CMS** is a web-based application consisting of a Reader Platform and an Admin CMS.

The Reader Platform focuses on:

* Discovering content
* Searching
* Filtering
* Reading chapters
* Tracking reading progress
* Bookmarking
* Reading history
* Chapter comments
* Recently added content
* Recently updated content
* Latest chapters

The Admin CMS focuses on:

* Managing series
* Managing genres
* Managing chapters
* Managing chapter pages
* Publishing content
* Managing users
* Moderating comments
* Monitoring basic system statistics

The initial system is designed around a generic `Series` entity that supports:

```text
Manga
Manhwa
Manhua
```

The MVP focuses on building a functional foundation for content management, content discovery, reading, user personalization, and basic community interaction.

Advanced features such as payment, subscription, AI recommendation, real-time chat, and native mobile applications are reserved for future development.

---

# End of Document

````