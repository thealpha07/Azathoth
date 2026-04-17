# Functional Requirements Document
**Project Name:** Azathoth 
**Document Owner:** Adarsh Sadanand (Admin / Developer)  
**Status:** Draft v1.0  

## 1. User Role Matrix
This matrix defines the baseline permissions across the platform's three access tiers. These rules govern all functional modules.

| Feature / Module           | Public (Guest) | Associates (Authenticated) | Admin                 |
| :------------------------- | :------------- | :------------------------- | :-------------------- |
| **Portfolio Landing Page** | Read           | Read                       | Read / Update         |
| **Public Forum**           | Read / Write   | Read / Write               | Read / Write / Delete |
| **Shared Vault**           | No Access      | Read                       | Read / Write / Delete |
| **Private Media Gallery**  | No Access      | Read                       | Read / Write / Delete |
| **Admin Command Center**   | No Access      | No Access                  | Read / Write / Delete |
| **Personal Blog**          | No Access      | No Access                  | Read / Write / Delete |

---

## 2. Module 1: Public Portfolio & Asset Retrieval
**Maps to:** BRD-01

### 2.1. FRD-PORT-01: Landing Page Rendering
**Description:** The system must render a static, responsive landing page detailing the developer's background, current tech stack, and project history.

* **Actor:** Public (Guest)
* **Pre-condition:** User navigates to the root domain (`https://adarshsadanand.in`).
* **Trigger:** Page load request.
* **Main Success Scenario:**
    1. The system serves the index page from GitHub Pages.
    2. The UI renders the Hero Section with a professional greeting.
    3. The UI renders the "About Me" section, outlining academic background at MSRIT and core competencies (Python, PostgreSQL, Snowflake, MongoDB).
    4. The UI renders the "Projects" grid, querying the static data array to display cards for key technical projects:
        * Medical Image Analysis (YOLOv2, CNN)
        * VR / Game Engine Mechanics (Unity/Unreal)
        * Deep Research Assistant (LLM Integration)
    5. The UI renders the Footer with links to the Public Forum and a "Contact Me" anchor.
* **Exception Paths:**
    * *E1: Asset Load Failure:* If an image or script fails to load, the system displays the fallback `alt` text and maintains the structural integrity of the layout without breaking the CSS grid.

### 2.2. FRD-PORT-02: Document Asset Retrieval (Resume)
**Description:** Visitors must be able to securely download the most current version of the public resume directly from the landing page.

* **Actor:** Public (Guest)
* **Pre-condition:** User is on the landing page and views the Hero or About section.
* **Trigger:** User clicks the "Download Resume" button.
* **Main Success Scenario:**
    1. User clicks the button.
    2. The system triggers a direct URL request to the public Supabase storage bucket where `resume_public_latest.pdf` is hosted.
    3. The browser initiates the file download to the user's local machine.
    4. The system logs a generic "Resume Downloaded" event in the telemetry tracking table (timestamp only, no PII collected).
* **Exception Paths:**
    * *E1: File Not Found (404):* If the resume file is missing from the storage bucket, the UI displays a localized toast notification: "The resume file is currently being updated. Please try again later." The system suppresses the default browser 404 error page to keep the user on the domain.

### 2.3. Module 1 Business Rules
* **BR-PORT-01:** The landing page must achieve a minimum Lighthouse performance score of 90 for mobile and desktop environments.
* **BR-PORT-02:** All images displayed on the public portfolio must be compressed to WebP format to reduce bandwidth consumption.