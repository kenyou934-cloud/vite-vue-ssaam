# SSAAM - Student School Activities Attendance Monitoring

## Overview
A Vue 3 + Vite frontend application for monitoring student attendance at school activities. This is a Single Page Application (SPA) that uses localStorage for data persistence.

## Project Structure
- **Framework**: Vue 3 with Composition API (script setup)
- **Build Tool**: Vite 5
- **Styling**: Tailwind CSS
- **Routing**: Vue Router 4
- **Data Storage**: Browser localStorage (no backend)

## Key Features
- User authentication (Login/Register)
- Admin account auto-initialization
- Student dashboard
- RFID code support for attendance
- Loading screen with school branding

## Configuration
- **Dev Server**: Port 5000, host 0.0.0.0
- **Vite Config**: Configured with `allowedHosts: true` for Replit proxy compatibility
- **Default Admin**: 
  - Email: admin@ssaam.edu
  - Student ID: admin
  - RFID: admin0000

## Development
The application is configured to run on Replit with:
- Automatic dependency installation via npm
- Dev server configured for Replit's proxy environment
- Static deployment configuration for production

## Recent Changes
- 2025-11-28: Admin security fix and developers popup feature
  - Fixed admin display name to hide last name (password) in Dashboard
  - Admin now shows only first name or 'Administrator' as fallback
  - Added "Meet Our Developers" popup in Login.vue, Register.vue, and Dashboard.vue
  - Clicking "CCS - Creatives Committee" shows popup with 5 developer profiles (2 backend, 2 frontend, 1 UI/UX designer)

- 2024-11-28: Initial import and Replit environment setup
  - Installed npm dependencies
  - Configured workflow for dev server
  - Set up static deployment configuration
  - Verified application runs successfully

## Architecture
This is a pure frontend application with no backend dependencies. All user data is stored in the browser's localStorage, making it suitable for prototyping and development.
