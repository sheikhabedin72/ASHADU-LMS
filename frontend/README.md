# ASHADU-LMS Frontend

Next.js 14 frontend for the ASHADU-LMS platform with Tailwind CSS styling.

## Quick Start

```bash
npm install
npm run dev
```

Application runs on http://localhost:3000

## Project Structure

```
app/
├── layout.js           # Root layout
├── page.js            # Home page
├── auth/              # Authentication pages
├── dashboard/         # Dashboard routes
├── courses/           # Course pages
└── admin/             # Admin pages

components/
├── ui/               # Reusable UI components
├── layout/           # Layout components
└── features/         # Feature-specific components

lib/
├── auth.js          # Authentication utilities
├── api.js           # API client
└── utils.js         # Utility functions

styles/
└── globals.css      # Global styles
```

## Features

- Next.js 14 with App Router
- Server-side rendering
- Tailwind CSS styling
- Authentication with NextAuth
- Redux state management