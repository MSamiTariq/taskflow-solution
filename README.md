# TaskFlow - MERN Stack Task Management Application

## Project Overview
This project is an implementation of the TaskFlow test, a MERN stack task management application with authentication, task management, filtering, and administrative features.

## Technologies Used
- **Frontend**: React, React Router, TailwindCSS
- **Backend**: Node.js, Express
- **Database**: MongoDB
- **Authentication**: JWT-based authentication
- **State Management**: React Context API and localStorage

### Prerequisites
- Node.js v20.14.0
- NPM v10.7.0
- MongoDB


## Test Problems
1. **Complete the tasks**:

△ Task 1 - Display Login/Register page before the landing page
- Users are should to login first to access the full list of tabs.
- When they're logged out, only Dashboard panel should to be displayed.

△ Task 2 - Task Filter
- Allow users to filter tasks based on their completion status (e.g., show only completed or incomplete tasks).
- Optional: Add a search feature to filter tasks by title.

△ Task 3 - Add User Log page on the Admin page
- Display the user logs(login time, logout time, JWT token name, user name, role, ip address)
- The user logs could be deleted by admin action - DELETE

2. **Commit Your Changes**:
- Make sure you commit your changes regularly:
    ```bash
    git add .
    git commit -m "Task1 completed!"
    git push origin main
    ```

3. **Submit Your Repository Link**:
- Once you’ve completed the tasks, send the result to https://forms.gle/1E2z5713vGV9vhr4A.
- Please make sure that your repository is **public** or share access if it's private.

4. **Deadline**:
  45 min ~ 1 hour


====================================================================================

  ## Tasks Completed
- Task 1: Login/Register shown before other pages; unauthenticated users see only a minimal Dashboard button.
  - Implemented with `PublicRoute` and `ProtectedRoute` in `src/App.jsx` and navbar logic in `src/components/common/Navbar.jsx`.
- Task 2: Task Filter page with status (All/Complete/Incomplete) and debounced search.
  - `src/components/tasks/TaskFilter.jsx` reads from `localStorage` `tasks` and updates live.
  - Linked from both Admin and User sidebars.
- Task 3: Admin User Logs show login/logout time, token name, username, role, IP; supports delete.
  - Logs created on login (`src/components/auth/Login.jsx`) and logout times recorded on sign-out (`src/contexts/AuthContext.jsx`).
  - View and manage at `Admin → User Logs` (`src/pages/AdminPages/UserLogPage.jsx`).

## How to Test
- Task 1: Visit `/` (you’ll see Login). After login, you land on your dashboard; logout collapses navbar to minimal state.
- Task 2: Open “Task Filter” from sidebar; change status filter and type in search. Debounce smooths typing.
- Task 3: Log in/out; check “User Logs” for entries with login/logout times; delete an entry to confirm removal.

## Notes
- This test uses localStorage for auth mock, tasks, and logs to keep scope frontend-focused.

## Implementation Notes (What I Did)
- Task 1: Enforced login-first and minimal UI when logged out.
  - Added `PublicRoute` to redirect authenticated users away from public pages and show Login first on `/`.
  - Kept `ProtectedRoute` for auth/role checks; moved `Landing` behind auth at `/landing`.
  - Navbar hides Task/Profile when logged out and shows a single Dashboard button linking to Login.
- Task 2: Implemented Task Filter with search and status filters, plus debounce.
  - `TaskFilter` reads from `localStorage` `tasks` and filters by All/Complete/Incomplete.
  - Added 300ms debounced search to avoid re-filtering on each keypress.
  - Linked from both Admin and User sidebars.
- Task 3: Built Admin User Logs with login/logout lifecycle and delete.
  - On login, append a log entry `{ id, userId, username, role, loginTime, logoutTime: null, tokenName, ipAddress }`.
  - On logout, update the latest unmatched log with `logoutTime`.
  - Admin can view/filter/sort/delete logs in `UserLogPage`.

### Key Files Touched
- `src/App.jsx` (Public/Protected routes)
- `src/components/common/Navbar.jsx` (logged-out UI)
- `src/components/tasks/TaskFilter.jsx` (filters + debounce)
- `src/components/admin/Sidebar.jsx`, `src/pages/UserPages/UserSidebar.jsx` (nav links)
- `src/components/auth/Login.jsx`, `src/contexts/AuthContext.jsx` (log lifecycle)