# Assignment Tracker - Spring 2026

**Live URL:** https://jjpatten14.github.io/assignment-tracker/assignment-tracker-cloud.html

A single-page web application for tracking college assignments across multiple courses with cross-device synchronization powered by Google Sheets.

## About

This tracker helps manage 140 assignments across 5 courses for Spring 2026 semester:
- **LAW-2010** - Business Law (21 assignments)
- **MAN-210** - Principles of Management (30 assignments)
- **SOS-1100** - Capstone (32 assignments)
- **MKT-2010** - Introduction to Marketing (31 assignments)
- **GOG-2300** - Geography (26 assignments)

## Features

- ✅ Track assignment completion with checkboxes
- 📊 Real-time statistics (total, completed, remaining, completion %)
- 🔍 Filter by course, week, status, or search by keyword
- 📅 Sort by due date, course, week, name, or type
- 📱 Mobile-friendly responsive design
- ☁️ **Cloud sync** - Check assignments on your phone, see updates on your laptop
- 💾 **Dual persistence** - Data saved to both Google Sheets AND localStorage for offline access

## Versions Available

### Cloud Sync Version (Recommended)
**URL:** https://jjpatten14.github.io/assignment-tracker/assignment-tracker-cloud.html

Syncs your progress across all devices using Google Sheets. Requires Google sign-in.

### Local-Only Version
**URL:** https://jjpatten14.github.io/assignment-tracker/assignment-tracker.html

Works completely offline using browser localStorage. No sign-in required, but data stays on one device only.

## Setup

For instructions on configuring Google Sheets sync, see [SETUP_INSTRUCTIONS.md](SETUP_INSTRUCTIONS.md)

## Technology

- Pure HTML/CSS/JavaScript (no frameworks)
- Google Sheets API for cloud storage
- Google Identity Services for OAuth authentication
- localStorage for offline backup
- Hosted on GitHub Pages

---

**Semester Start:** Monday, January 5, 2026
**Total Assignments:** 140
