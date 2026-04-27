# Business Requirements Document (BRD)
**Project Name:** Azathoth (adarshsadanand.in)  
**Document Owner:** Aditya (Admin / Developer)  
**Status:** Draft v1.1

## 1. Executive Summary
This project outlines the development of a multi-tiered web platform for adarshsadanand.in. The platform functions as a hybrid system, combining a public-facing professional portfolio with a secure, authenticated backend. It is designed to facilitate professional networking, community discussion, private data management, and remote infrastructure administration under a single domain.

## 2. Business Objectives
* **Professional Presence:** Establish a public landing page to showcase resumes, projects, and professional background.
* **Community Engagement:** Provide an open forum for public interaction and topic discussion.
* **Secure File Management:** Replace external cloud drives with a self-hosted, secure vault for coursework, personal documents, and media.
* **Controlled Data Sharing:** Implement strict Role-Based Access Control (RBAC) to allow specific users access to curated files and media galleries.
* **Remote Workspace Integration:** **Remote Workspace Integration:** Establish a secure, zero-trust remote access gateway to an Oracle Cloud Infrastructure (OCI) Ubuntu environment using Cloudflare Tunnels for secure system administration.

## 3. Target Audience
* **General Public / Recruiters:** Accessing the landing page, resume downloads, and public forum.
* **Known Associates:** Accessing shared folders and the private image gallery.
* **System Administrator:** Managing the entire platform, utilizing the private drive, publishing to the private blog, and accessing the remote OCI environment.

## 4. Scope Requirements
### 4.1. In-Scope
* Development of a responsive UI adhering to strict typography and spacing rules.
* Implementation of a unified authentication gateway to handle the three-tier access system (Public, Associates, Admin).
* Integration with Supabase for user authentication and PostgreSQL database management.
* Deployment of static assets via GitHub Pages and dynamic functions via Vercel.
* Secure routing for contact inquiries and document retrieval.
* Basic system telemetry and event logging for access control verification.
	* Integration of Cloudflare Zero Trust and `cloudflared` tunnels for secure, outbound-only remote access to the OCI instance.

### 4.2. Out-of-Scope (For v1.0)
* E-commerce or payment gateway integrations.
* Real-time chat features (outside of standard forum threading).
* Automated social media cross-posting.

## 5. High-Level Business Requirements (Mapped to RTM)

* **BRD-01 (Public Portfolio & Asset Retrieval):** The system must provide a public landing page detailing the owner's professional background and include dedicated, up-to-date download links for the owner's resume.
* **BRD-02 (Public Discussion Forum):** The system must host an open forum allowing guest read/write access for threaded discussions.
* **BRD-03 (Unified Access Control):** The system must implement a centralized login portal that authenticates users and strictly routes them based on their assigned RBAC tier (Associates vs. Admin).
* **BRD-04 (Tiered File Vault):** The system must provide a secure file management module. The Admin tier must have full read/write access to a private drive, while the Associates tier only receives read access to specific, admin-designated shared folders.
* **BRD-05 (Private Media Gallery):** The system must provide an image and media gallery explicitly restricted to the Associates and Admin tiers.
* **BRD-06 (Admin Publishing Module):** The system must feature a personal blog module restricted exclusively to Admin read/write access.
* **BRD-07 (Inbound Communications):** The system must include a functional "Contact Me" module that routes external inquiries directly to the system administrator without exposing backend email addresses.
* **BRD-08 (Audit & Governance Logging):** The system must log critical authentication events, failed access attempts, and system errors to maintain a secure and auditable baseline.
* **BRD-09 (Remote Workspace Gateway):** The system must provide the Admin tier with highly secure, clientless remote access to an OCI-hosted Ubuntu development environment, mediated strictly through an identity-aware Zero Trust network.