Doctor Booking Frontend
React + TypeScript frontend for a doctor appointment booking system, inspired by platforms like RedBus/BookMyShow. It provides separate views for admins and patients and connects to a Node.js/Express/Postgres backend.

Tech Stack
React + TypeScript

Vite

React Router DOM

Context API (auth + basic global state)

Fetch API for HTTP calls

Project Setup
Folder Structure (high level)
src/

App.tsx – main app + routes

AuthContext.tsx – authentication and user role state

api.ts – API base URL helper (VITE_API_BASE_URL)

pages/

HomePage.tsx

FindDoctorsPage.tsx

DoctorDetailsPage.tsx

BookingPage.tsx

MyBookingsPage.tsx

AdminPage.tsx

LoginPage.tsx

components/ (if any shared components)

styles.css / similar

Installation (local)
bash
git clone https://github.com/<your-username>/doctor-booking-frontend.git
cd doctor-booking-frontend
npm install
Environment Variables
Create .env in the project root:

text
VITE_API_BASE_URL=http://localhost:4000
For production, set VITE_API_BASE_URL to the deployed backend URL, e.g.:

text
VITE_API_BASE_URL=https://doctor-booking-backend-r6t2.onrender.com
Running the App Locally
bash
npm run dev
Then open the URL printed by Vite (usually http://localhost:5173).

The frontend will call the backend at VITE_API_BASE_URL via the apiUrl helper.

Deployed URLs
Frontend: https://doctor-booking-frontend2-git-main-santhosh-s-projects-651f9c28.vercel.app?_vercel_share=AzlN8DJrknJ46PMP5Ys94AZbIdCQR49U

Backend: https://doctor-booking-backend-r6t2.onrender.com

(Replace with your actual deployment URLs.)

Test Credentials
Patient
Email: patient_initial@example.com

Password: admin123

Admin
Email: admin_initial@example.com

Password: admin123

Use these credentials on the Login page.

Main Features
Patient (User) Features
View list of doctors with specialization and city.

View detailed doctor profile.

See calendar-style grouped slots (by date) for each doctor.

Select a time slot and enter a reason for visit.

Book an appointment (PENDING booking).

Confirm booking via fake payment (status becomes CONFIRMED).

View all bookings in My Bookings page:

Doctor, date/time, reason, status, payment status.

Cancel an appointment.

Reschedule an appointment to another available slot.

Admin Features
Create doctors (name, specialization, city, consultation type, fee, rating).

View all doctors in a table.

Create slots for a selected doctor (start/end time).

View and delete slots for that doctor.

Routing
/ – Home page + next appointment card for logged-in patient.

/login – Login as patient or admin.

/find-doctors – Browse doctors.

/doctor/:doctorId – Doctor details page.

/booking/:doctorId – Booking page (calendar-style slots + reason).

/my-bookings – Patient bookings list.

/admin – Admin dashboard (doctors + slots management).

API Integration
The frontend uses src/api.ts:

ts
const API_BASE_URL =
  import.meta.env.VITE_API_BASE_URL || "http://localhost:4000";

export function apiUrl(path: string) {
  if (!path.startsWith("/")) path = "/" + path;
  return API_BASE_URL + path;
}
All pages call fetch(apiUrl("/api/...")), so switching between local and production only requires changing VITE_API_BASE_URL.

Main endpoints used:

GET /api/doctors

GET /api/doctors/:id/slots

POST /api/admin/doctors

POST /api/admin/doctors/:id/slots

DELETE /api/admin/doctors/:id

DELETE /api/admin/doctors/:id/slots/:slotId

POST /api/doctors/:doctorId/slots/:slotId/bookings

POST /api/payments/fake

PATCH /api/bookings/:id/cancel

PATCH /api/bookings/:id/reschedule

GET /api/patients/bookings?email=...

POST /api/auth/login (for JWT login)

Known Limitations / Future Improvements
Simple mock authentication and basic role handling.

No real payment gateway (uses a fake payment endpoint).

No real-time updates (WebSockets) yet; could add polling or sockets for live slot updates.

UI/UX can be extended for mobile responsiveness and accessibility.