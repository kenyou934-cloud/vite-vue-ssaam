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

## Recent Changes (2025-11-28)

### Professional SVG Icon System
- Replaced ALL emojis with professional SVG icons throughout Registration, Login, and Dashboard
- Icons include: user.svg, key.svg, mail.svg, register_user.svg, arrow_down.svg, course.svg, book.svg, detector.svg, calendar.svg, event_note.svg, home.svg, logout.svg, help.svg
- White icon filtering: `style="filter: brightness(0) invert(1);"` for sidebar/gradient backgrounds

### Registration Form Icons
- **First/Middle/Last Name**: user.svg
- **Email**: mail.svg
- **Suffix Dropdown**: arrow_down.svg (right-aligned indicator)
- **Student ID**: user.svg
- **RFID Code**: detector.svg
- **Year Level**: book.svg
- **Program**: course.svg
- **Semester**: calendar.svg
- **School Year**: event_note.svg
- **Register Tab**: register_user.svg (white background)

### Dashboard & Navigation
- **Home Icon**: home.svg (white filter in sidebar)
- **Logout Icon**: logout.svg (white filter in sidebar, replaces 🚪 emoji)
- **Help Button**: help.svg icon (responsive placement)
  - Desktop: Fixed floating button (top-right, purple/pink gradient)
  - Mobile: In header next to hamburger menu with hover state

### Contact/Help System
- **Help Modal** ("Need Help?"): 
  - Accessible from both Login page and Dashboard
  - Shows: Email Support, JRMSU CCS Office, Meet Our Developers, Quick Help tips
  - Responsive design with gradient accent boxes
  - Same styling across both Login and Dashboard

### Login Dashboard Updates
- **Register Button**: Now uses user.svg instead of 👤 emoji
- **Password Visibility**: Removed animation, clean toggle only
- **Help Link**: Changed to help.svg button with inline styling
- **Contact Modal**: Added to Login.vue for consistency

### Dashboard Updates
- **Mobile Header**: Help button with rounded hover state
- **Desktop Help Button**: Floating button with gradient background
- **Both Sidebars**: White home and logout icons with proper filtering
- **Responsive**: Help button adapts to screen size

## Previous Changes (Earlier 2025-11-28)

### Image Compression
- Client-side image compression using Canvas API
- Automatic compression to 1MB or below before uploading
- Smart quality reduction: starts at 0.9, decreases by 0.08 per attempt
- Maintains aspect ratio and maximum 1920x1920 dimensions

### Styled Notifications & Security
- Replaced all alert() with styled error modal ("Oops!" header)
- Anti-copy protection: disabled text selection, blocked right-click/shortcuts
- Form inputs preserved with normal text selection

### Admin Security & Developers Popup
- Fixed admin display name to hide password
- "Meet Our Developers" popup with 5 developer profiles
- Accessible from Login, Register, and Dashboard

## Architecture
Pure frontend application with no backend. All user data stored in browser's localStorage. Suitable for prototyping and development with comprehensive UI/UX polish.
