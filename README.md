# Parking Tracker

An internal web application designed to simplify and automate the process of booking parking spots at company offices. The MVP version delivers core functionalities that allow employees to independently book, view, and cancel parking spot reservations.

## Tech Stack

### Frontend

- **Astro 5** - Modern web framework for building fast, content-focused websites
- **React 19** - UI library for building interactive components
- **TypeScript 5** - Type-safe JavaScript with enhanced IDE support
- **Tailwind CSS 4** - Utility-first CSS framework for styling
- **Shadcn/ui** - Library of accessible React components
- **Konva.js** - 2D graphics library for creating interactive parking lot maps

### Backend

- **Supabase** - Comprehensive backend-as-a-service solution providing:
  - PostgreSQL database
  - Built-in user authentication (Supabase Auth)
  - SDKs for multiple programming languages
  - Open-source and self-hostable

### AI Integration

- **OpenRouter.ai** - Access to multiple AI models (OpenAI, Anthropic, Google, etc.) for communication and automation features

### CI/CD & Hosting

- **GitHub Actions** - CI/CD pipeline automation
- **DigitalOcean** - Cloud hosting via Docker containers

## Getting Started Locally

### Prerequisites

- Node.js v22.14.0 (as specified in `.nvmrc`)
- npm (comes with Node.js)

### Installation

1. Clone the repository:

```bash
git clone <repository-url>
cd parking-tracker
```

2. Install dependencies:

```bash
npm install
```

3. Set up environment variables:
   - Copy `.env.example` to `.env`
   - Configure Supabase credentials and other required environment variables

4. Run the development server:

```bash
npm run dev
```

5. Open [http://localhost:4321](http://localhost:4321) in your browser

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally
- `npm run astro` - Run Astro CLI commands
- `npm run lint` - Run ESLint for code quality checks
- `npm run lint:fix` - Automatically fix ESLint issues
- `npm run format` - Format code with Prettier

## Project Scope

### Core Features (MVP)

#### User Management

- **Authentication**: Supabase Auth integration for secure employee login
- **User Roles**: Two roles available:
  - **Employee**: Book, view, and cancel their own reservations
  - **Administrator**: All employee permissions plus access to admin panel
- **User Profiles**: Manage personal information including:
  - First Name, Last Name
  - Team Name, Default Office
  - Vehicle License Plate, Brand/Model

#### Booking System

- **Single Booking Policy**: Users can book one parking spot per day
- **Advance Booking**: Bookings can be made up to 7 business days in advance
- **Cancellation Window**: Bookings can be canceled until 3:00 AM on the booking day
- **Interactive Map**: HTML/CSS/React-Konva based parking lot visualization
- **Spot Selection**: Users select specific parking spots from an interactive map

#### User Interface

- **Calendar View**: Select booking dates with availability overview
- **Location Selection**: Choose office and parking level
- **Parking Map**: Interactive visualization showing spot status (available, taken, out of service)
- **My Bookings**: View and manage upcoming/past reservations

#### Admin Panel

- **Spot Management**: Enable/disable individual parking spots
- **Maintenance Mode**: Temporarily take spots out of service
- **Real-time Updates**: Changes reflect immediately for all users

### Out of Scope (Future Versions)

- No-shows handling and penalties
- Waitlist functionality
- In-app role management (handled via Supabase admin panel)
- Mobile applications (iOS/Android)
- Dynamic parking lot configuration (requires developer intervention)

## Project Status

This is the **Minimum Viable Product (MVP)** version of Parking Tracker, focused on delivering essential parking booking functionality for company employees. The application is optimized for laptop use and provides a solid foundation for future enhancements.

### Success Metrics

- **Primary KPI**: Percentage of active users making at least 4 bookings per month
- **Supporting Metrics**:
  - Parking occupancy rates across different days and offices
  - User adoption rate among eligible employees
  - Individual spot utilization patterns

## License

MIT
