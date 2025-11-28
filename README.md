# React Events – TanStack React Query Integration

This project demonstrates a modern approach to **data fetching, caching, mutation, and synchronization** in React applications using **@tanstack/react-query** together with **React Router**.  
It provides a full-featured event management interface where users can create, edit, view, search, and delete events through a RESTful API built on Express.js.

---

## ⚙️ Core Concept

The main focus is on **React Query hooks** and their interaction with React Router’s navigation system.  
Each part of the app showcases a specific pattern of managing asynchronous state in a declarative and predictable way.

---

## 📸 Project Preview

<h3 align="center">📸 Screenshots</h3>

<p align="center">
  <img src="https://raw.githubusercontent.com/Figrac0/tanstack-react-query/main/src/assets/1.png" alt="Preview 1" width="450"/><br/>
</p>
<p align="center">
  <img src="https://raw.githubusercontent.com/Figrac0/tanstack-react-query/main/src/assets/2.png" alt="Preview 2" width="450"/><br/>
</p>
<p align="center">
  <img src="https://raw.githubusercontent.com/Figrac0/tanstack-react-query/main/src/assets/3.png" alt="Preview 3" width="450"/><br/>
</p>
<p align="center">
  <img src="https://raw.githubusercontent.com/Figrac0/tanstack-react-query/main/src/assets/4.png" alt="Preview 4" width="450"/><br/>
</p>
<p align="center">
  <img src="https://raw.githubusercontent.com/Figrac0/tanstack-react-query/main/src/assets/5.png" alt="Preview 5" width="450"/><br/>
</p>

---

## 🔍 React Query Usage Overview

### `useQuery`
Used throughout the project to **fetch and cache event data** from the backend API.  
- Fetches lists of events (`fetchEvents`) and single event details (`fetchEvent`).  
- Handles loading, error, and success states automatically.  
- Uses `queryKey` and `queryFn` patterns for deterministic cache updates.  
- Enables features like automatic refetching and background synchronization.

Examples of usage:
- `NewEventsSection`: fetches the latest events.
- `FindEventSection`: fetches filtered events by search term.
- `EventDetails` and `EditEvent`: fetch detailed data of a selected event.

---

### `useMutation`
Used to **perform side-effect operations** such as creating, updating, and deleting events.  
- `createNewEvent` (POST)
- `updateEvent` (PUT)
- `deleteEvent` (DELETE)

Each mutation:
- Provides real-time UI feedback through pending and error states.
- Integrates `onSuccess`, `onError`, and `onSettled` callbacks to update the cache.
- Works together with `queryClient.invalidateQueries()` to refetch data after mutations.

---

### `queryClient`
Configured globally to control cache and invalidate queries when needed.  
- Centralized in `util/https.js`.
- Used after successful mutations to keep all event lists up-to-date without manual refetching.
- Provides access to optimistic updates (used in `EditEvent` with rollback on failure).

---

## 🔄 React Router Integration

The project combines React Router with React Query to handle:
- Modal routing (creating and editing events as modals using `<dialog>` + portals).
- Data fetching that responds to navigation changes.
- Seamless transitions between pages (`/events`, `/events/:id`, `/events/new`, `/events/:id/edit`).

Each route is connected to corresponding React Query operations, ensuring minimal network calls and instant state recovery.

---

## 🧱 Backend (Express.js)

The backend API serves JSON data from a local `events.json` file.  
It supports:
- `GET /events` – Fetch all or filtered events.
- `GET /events/:id` – Fetch single event details.
- `POST /events` – Create a new event.
- `PUT /events/:id` – Update an event.
- `DELETE /events/:id` – Remove an event.
- `GET /events/images` – Fetch selectable images for event cards.

The Express server implements artificial delay and proper error responses to emulate real-world latency and validation behavior.

---

## 🧩 Components Overview

- **Header** – Displays navigation with React Query loading indicator (`useIsFetching`).
- **Modal** – Custom portal-based component for editing and creation dialogs.
- **EventForm** – Handles form inputs and integrates `ImagePicker` with server-fetched images.
- **EventDetails** – Uses query caching for single-event details and handles deletions with modal confirmation.
- **ErrorBlock / LoadingIndicator** – Standardized components for consistent feedback across all query states.

---

## 🎯 Project Goals

- Demonstrate how **React Query** simplifies API communication compared to manual `useEffect` + `fetch`.
- Show how **caching, background refetching, and optimistic updates** create a fluid user experience.
- Integrate query-driven UI updates directly with **React Router** transitions and modals.

---

## 🧠 Key React Query Hooks in Context

| Hook | Purpose | Example Usage |
|------|----------|----------------|
| `useQuery` | Fetch and cache data | Events list, event details |
| `useMutation` | Trigger writes to the server | Create, update, delete events |
| `useIsFetching` | Global loading feedback | Header progress bar |
| `queryClient.invalidateQueries` | Refresh cached data after mutations | After successful event creation or update |

---



## 🚀 Technologies

- **React 19**
- **React Router 6**
- **@tanstack/react-query v5**
- **Express.js (Node.js backend)**
- **Vite build system**

---

## 🧩 Summary

This project is a practical showcase of integrating **React Query** into a **React Router-based SPA**, demonstrating:
- Declarative asynchronous data handling.
- Optimistic updates and error boundaries.
- Centralized cache management with minimal boilerplate.
- Scalable architecture ready for production-level CRUD applications. 
