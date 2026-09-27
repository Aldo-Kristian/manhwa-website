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
- Browse series
- Search for series
- Filter series
- View series details
- View chapter lists
- Read chapters
- Navigate between chapters
- Bookmark series
- Track reading history
- Continue reading
- Comment on chapters
- Discover recently added content
- Discover recently updated content
- Discover latest chapters

### Admin CMS

The Admin CMS allows administrators to:

- Authenticate
- Manage series
- Manage genres
- Manage chapters
- Upload chapter pages
- Manage page order
- Publish and unpublish chapters
- Manage users
- Moderate comments
- View basic system statistics

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