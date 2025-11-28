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

### Contact Modal - Final Improvements
- **Responsive Grid Layout**: Mobile (1 col) → Tablet (2 col) → Desktop (3 col)
- **Scrollable on Small Screens**: Added `max-h-[90vh] overflow-y-auto`
- **Form Validation Compatibility**: Modal z-index set to `z-40` (allows validation messages to appear)
- **All SVG Icons White**: mail.svg, home.svg, register_user.svg with brightness filter

### Developers Popup - Fixed Overlapping Text
- **Larger Modal**: Increased to `max-w-4xl` for better spacing
- **Bigger Avatar Circles**: `w-20 h-20` (was `w-16 h-16`)
- **Smart Text Truncation**:
  - Developer names: `line-clamp-2` (max 2 lines)
  - Roles: `line-clamp-1` (max 1 line)
- **Better Responsive Grid**: `grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5`
- **Increased Gap Spacing**: `gap-6` for better layout

### Login Dashboard Updates
- **Register Button Icon**: Changed from `user.svg` to `register_user.svg` (both desktop & mobile)
- Applied across all UI sections for consistency

### Professional SVG Icon System (Complete)
- **All Emojis Replaced**: user.svg, key.svg, mail.svg, register_user.svg, arrow_down.svg, course.svg, book.svg, detector.svg, calendar.svg, event_note.svg, home.svg, logout.svg, help.svg
- **White Icon Filter**: `filter: brightness(0) invert(1);` for sidebar/gradient backgrounds
- **Consistent Across All Pages**: Login, Register, Dashboard, and Modals

## Architecture
Pure frontend application with no backend. All user data stored in browser's localStorage. Suitable for prototyping and development with comprehensive UI/UX polish and professional icon system.
