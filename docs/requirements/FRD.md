# Functional Requirements Document (FRD)
**Project Name:** Azathoth  
**Document Owner:**  Admin / Developer
**Status:** Draft v1.1

## 1. User Role Matrix
This matrix defines the baseline permissions across the platform's features.

| Feature / Module           | Public (Guest) | Associates (Authenticated) | Admin                 |
| :------------------------- | :------------- | :------------------------- | :-------------------- |
| **Portfolio & Contact**    | Read / Submit  | Read / Submit              | Read / Update         |
| **Public Forum**           | Read / Write   | Read / Write               | Read / Write / Delete |
| **Shared Vault & Gallery** | No Access      | Read                       | Read / Write / Delete |
| **Admin Command Center**   | No Access      | No Access                  | Read / Write / Delete |
| **Personal Blog**          | No Access      | No Access                  | Read / Write / Delete |
| **OCI Remote Gateway**     | No Access      | No Access                  | Full Access           |

---

## 2. Module 1: Public Interface & Communications
**Maps to:** BRD-01, BRD-07

### 2.1. FRD-PORT-01: Landing Page Rendering
* **Actor:** Public (Guest)
* **Trigger:** User navigates to the root domain.
* **Main Success Scenario:**
    1. System serves the static index page.
    2. Renders "About Me" detailing academic background, work and tech stack.
    3. Renders "Projects" grid with cards for key technical work.
* **Exception Path:**
    * *E1: Asset Load Failure:* System displays fallback text and maintains grid integrity.

### 2.2. FRD-PORT-02: Secure Asset Retrieval (Resume)
* **Actor:** Public (Guest)
* **Trigger:** User clicks "Download Resume".
* **Main Success Scenario:**
    1. System triggers a request to the Supabase storage bucket (`resume_public_latest.pdf`).
    2. File downloads to the local machine.
* **Exception Path:**
    * *E1: File Missing (404):* System suppresses default 404 and displays a toast notification: "Resume updating. Please try again later."

### 2.3. FRD-COM-01: Inbound Contact Form
* **Actor:** Public (Guest)
* **Trigger:** User submits the "Contact Me" form (Name, Email, Message).
* **Main Success Scenario:**
    1. Frontend validates email format.
    2. Payload is sent to a Vercel serverless function.
    3. Function writes the record to the Supabase `inquiries` table.
    4. System displays a success message: "Message received. I will reach out shortly."

---

## 3. Module 2: Authentication, Routing & Governance
**Maps to:** BRD-03, BRD-08

### 3.1. FRD-AUTH-01: Unified Login Flow
* **Actor:** Unauthenticated User
* **Trigger:** User enters credentials and clicks "Sign In".
* **Main Success Scenario:**
    1. Payload is sent to Supabase Auth endpoint.
    2. Supabase validates and returns a JWT containing the user's `role_id`.
    3. System reads `role_id` and redirects:
        * If `role_id == associate` -> Redirects to `/shared-vault`.
        * If `role_id == admin` -> Redirects to `/admin-dashboard`.
    4. System logs a successful login event in the `audit_logs` table.
* **Exception Paths:**
    * *E1: Invalid Credentials:* System clears password field and displays "Invalid email or password." Logs failed attempt.
    * *E2: Rate Limiting:* After 5 failed attempts, Supabase locks the account for 15 minutes.

---

## 4. Module 3: Community & Forum
**Maps to:** BRD-02

### 4.1. FRD-FORUM-01: Read & Write Threads
* **Actor:** Public / Associates
* **Trigger:** User submits a new post to the Public Forum.
* **Main Success Scenario:**
    1. User enters a Title and Body.
    2. System sanitizes input (stripping malicious HTML/scripts).
    3. Record is inserted into the Supabase `forum_posts` table.
    4. UI instantly updates to display the new thread.
* **Business Rule:** Unauthenticated forum posts are limited to 500 characters to mitigate spam.

---

## 5. Module 4: The Vault & Media Gallery
**Maps to:** BRD-04, BRD-05

### 5.1. FRD-VAULT-01: Associate Read-Only Access
* **Actor:** Associate
* **Trigger:** User navigates to `/shared-vault`.
* **Main Success Scenario:**
    1. System verifies the active JWT `role_id`.
    2. System queries the Supabase storage bucket specifically mapped to the Associate tier.
    3. Renders a file tree UI displaying approved folders and an image grid for the Gallery.
    4. User can click to preview or download files.
* **Exception Path:**
    * *E1: Unauthorized Access:* If a guest attempts to hit the route, the middleware intercepts and redirects to `/login`.

### 5.2. FRD-VAULT-02: Admin Drive Management
* **Actor:** Admin
* **Trigger:** Admin uploads a document (e.g., MTech coursework, PDF).
* **Main Success Scenario:**
    1. Admin drags and drops a file into the `/admin-dashboard/drive` UI.
    2. System streams the file to the secure Admin bucket in Supabase.
    3. UI displays a progress bar, then updates the file list upon successful upload.

---

## 6. Module 5: Admin Utilities & Infrastructure
**Maps to:** BRD-06, BRD-09

### 6.1. FRD-BLOG-01: Personal Blog Publishing
* **Actor:** Admin
* **Trigger:** Admin saves a new post in the Private Blog editor.
* **Main Success Scenario:**
    1. Admin writes content using a Markdown editor component.
    2. Post is saved to the `private_blog` table.
    3. System renders the Markdown into HTML for the Admin reading view.

### 6.2. FRD-GATEWAY-01: OCI Remote Workspace Access
* **Actor:** Admin
* **Trigger:** Admin clicks the "Launch Workspace" button in the Admin Dashboard.
* **Main Success Scenario:**
    1. System validates the Admin JWT.
    2. System initiates a secure proxy connection to the Apache Guacamole instance hosted on the OCI Ubuntu server.
    3. The Ubuntu desktop environment renders seamlessly within an HTML5 canvas in the browser.
    4. Admin can interact with the remote terminal and GUI without installing local client software.
* **Exception Path:**
    * *E1: Instance Unreachable:* If the OCI server is down, the system displays: "Remote instance unavailable. Check cloud console status."