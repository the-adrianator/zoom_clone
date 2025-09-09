## Xoom — Video Conferencing App (Zoom‑style)

Xoom is a Zoom‑style video conferencing web app built with Next.js 14 and Stream's Video SDK. It supports secure authentication with Clerk, scheduling and joining meetings (including a personal room), and a modern in‑call experience with multiple layouts, device controls, participant list, and call stats.

Live features implemented in this repo are focused on client and server integration with Stream for real‑time video, plus a clean UI using Tailwind CSS and shadcn/ui (Radix primitives).

## Features

- Modern home dashboard with time/date and quick actions
- Authentication (sign in/up) and protected routes via Clerk
- Personal meeting room with shareable invite link
- Create/join meetings powered by Stream Video SDK
- Pre‑join setup: video preview, device settings, mic/cam toggles
- In‑call controls: leave/end call, participant list, call stats
- Multiple layouts: grid, speaker‑left, speaker‑right
- Upcoming and previous meetings views (via Stream call queries)
- Recordings view placeholder (data surface prepared)

## Tech Stack

- Next.js 14 (App Router)
- React 18
- TypeScript
- Tailwind CSS + tailwind-merge + tailwindcss-animate
- shadcn/ui components (Radix UI primitives)
- Stream Video SDK (`@stream-io/video-react-sdk`, `@stream-io/node-sdk`)
- Clerk for authentication (`@clerk/nextjs`)
- lucide-react icons
- react-datepicker

## Project Structure

- `app/` — App Router pages, layouts, and route groups
  - `(auth)/sign-in`, `(auth)/sign-up` — Auth routes (Clerk)
  - `(root)/(home)` — Home dashboard and sections (`upcoming`, `previous`, `recordings`, `personal-room`)
  - `meeting/[id]` — Meeting room route
- `components/` — UI and feature components (MeetingRoom, MeetingSetup, modals, ui/*)
- `hooks/` — Custom hooks for Stream calls (e.g., `useGetCalls`, `useGetCallById`)
- `actions/` — Server actions (e.g., Stream token provider)
- `providers/` — Context providers (e.g., `StreamClientProvider`)
- `constants/` — Static configuration (sidebar links, avatars)
- `middleware.ts` — Route protection via Clerk

## Environment Variables

Create a `.env.local` with the following keys:

```bash
# Stream Video
NEXT_PUBLIC_STREAM_API_KEY=your_stream_api_key
STREAM_SECRET_KEY=your_stream_secret

# App URL used for invitation links
NEXT_PUBLIC_BASE_URL=http://localhost:3000

# Clerk Auth
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
```

## Getting Started

Install dependencies:

```bash
npm install
# or
yarn
```

Run the development server:

```bash
npm run dev
# or
yarn dev
```

Open `http://localhost:3000` in your browser.

## Usage Notes

- Authentication is required to access protected routes like `/`, `/upcoming`, `/previous`, `/recordings`, `/personal-room`, and `/meeting/*` (enforced in `middleware.ts`).
- Tokens for Stream are generated server‑side via a server action in `actions/stream.actions.ts` and consumed by `providers/StreamClientProvider.tsx`.
- The personal room link uses `NEXT_PUBLIC_BASE_URL` and your Clerk user ID to construct the URL.

## Scripts

- `dev` — Start Next.js in development
- `build` — Build for production
- `start` — Start the production server
- `lint` — Run linting

## License

This project is for learning/portfolio purposes.
