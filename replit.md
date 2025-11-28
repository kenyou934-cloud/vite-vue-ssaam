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
- Student dashboard with responsive design
- RFID code support for attendance
- Professional SVG icon system throughout
- Help/Contact modal accessible from Login and Dashboard
- Mobile hamburger menu with smooth animations
- Anti-copy protection and styled error notifications
- Image preloading before login form appears
- Optional field labels for better UX

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

## Latest Updates (2025-11-28)

### Image Preloading & Optional Fields
- **Loading Screen Image Preload**: All images (SVG icons, background, logo) now preload before proceeding to login
  - Implemented in LoadingScreen.vue with Promise.all()
  - Prevents image flashing or delays during user interactions
  - Graceful error handling for missing images
- **Optional Field Labels**: Register form now clearly marks optional fields
  - Middle Name: Shows "(optional)" in gray text
  - RFID Code: Shows "(optional)" in gray text
  - Applied to both desktop and mobile versions
  - Helps users understand required vs. optional information

### Contact Modal - Fully Responsive
- **Grid Layout**: Mobile (1 col) → Tablet (2 col) → Desktop (3 col)
- **Scrollable on Small Screens**: Added `max-h-[90vh] overflow-y-auto`
- **Form Validation Compatibility**: Modal z-index set to `z-40`
- **All SVG Icons White**: mail.svg, home.svg, register_user.svg

### Developers Popup - Fixed Text Overlap
- **Larger Modal**: `max-w-4xl` for better spacing
- **Bigger Avatar Circles**: `w-20 h-20`
- **Smart Text Truncation**:
  - Developer names: `line-clamp-2`
  - Roles: `line-clamp-1`
- **Better Responsive Grid**: `grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5`

### Login Dashboard Updates
- **Register Button Icon**: Uses `register_user.svg` (both desktop & mobile)

### Professional SVG Icon System (Complete)
- **All Icons**: user.svg, key.svg, mail.svg, register_user.svg, arrow_down.svg, course.svg, book.svg, detector.svg, calendar.svg, event_note.svg, home.svg, logout.svg, help.svg
- **White Icon Filter**: `filter: brightness(0) invert(1);` for modals
- **Consistent Across All Pages**

## Architecture
Pure frontend application with no backend. All user data stored in browser's localStorage. Enhanced with image preloading for smooth UX and optional field indicators for better form usability.
