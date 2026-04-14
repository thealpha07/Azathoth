This repository contains the source code and project documentation for my personal web platform, live at adarshsadanand.in.

The goal of this project is to build a complete, multi-tiered website that serves as a public portfolio, a private file drive, and a community forum. While it is a solo project, it is structured and documented like a standard development project.

Access and Features
The site is divided into three access levels:

	Public Access

		Landing Page: A straightforward portfolio, basic greetings, and an "About Me" section.

		Public Forum: A space where visitors can read, write, and discuss topics.

	Friends Login

		Shared Files: Access to specific shared folders.

		Gallery: A private image gallery.

	Personal Login (Admin)

		Drive: Secure cloud storage for personal files, college documents, MTech coursework, and resumes.

		Personal Blog: A private space for notes and personal writing.

Tech Stack
The architecture is split to handle static pages, server-side logic, and database management efficiently.

	Domain: adarshsadanand.in

	Frontend Hosting: GitHub Pages (for static and public-facing pages).

	Application Hosting: Vercel (for dynamic routing and API handling).

	Backend & Database: Supabase (utilizing PostgreSQL for user authentication, file storage metadata, and forum data).

	Scripting & Logic: Python and JavaScript/TypeScript (depending on Vercel serverless function requirements).

Project Guidelines
	To maintain a clean and usable project, all code, documentation, and user interfaces must adhere to the following rules:

Documentation
To treat this as a formal development project, the software development lifecycle is documented in the /QMS folder.

	BRD (Business Requirements Document): What the site needs to achieve.

	FRD (Functional Requirements Document): How the features (logins, forums, file uploads) work.

	TRD (Technical Requirements Document): How the GitHub Pages, Vercel, and Supabase integration is structured.

	CRD (Component Requirements Document): The UI components, design system, and typography rules.

	Test Results: The checklist for bug tracking, QA, and testing the login tiers.

Local Development
	Clone the repository.

	Install dependencies (refer to package manager instructions in the root).

	Set up your local .env file with the Supabase API keys and Vercel environment variables.

	Run the local development server.