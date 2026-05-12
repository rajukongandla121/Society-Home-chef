# Society HomeChef MVP

A hyperlocal home-chef ordering platform built for gated societies. This MVP demonstrates a complete 3-role flow (HomeChef, Resident, Rider) with AI-simulated nutrition estimation, robust matching logic, and a premium UI.

## Architecture & Tech Choices

### Tech Stack
- **Frontend/Logic**: Vanilla HTML, CSS, and JavaScript. 
- **Database / State Management**: `localStorage` (Browser-native local storage).
- **Deployment**: Local HTML file (zero-config, runs anywhere).

**Justification:**
Given the constraints and the goal of demonstrating product thinking and system design, a Vanilla JS Single Page Application (SPA) with `localStorage` was chosen. This entirely eliminates environment setup issues, dependency conflicts, or backend hosting complexities. It allows reviewers to instantly run and test the end-to-end flow simply by opening the `index.html` file in any modern browser. The UI uses modern CSS variables, Flexbox/Grid, and glassmorphism to deliver a highly polished, responsive experience without heavy CSS frameworks.

### Data Model & Roles
The system revolves around three core entities acting within the same "society":
1. **Users**: Stores profile info, role (`chef`, `resident`, `rider`), and simulated GPS coordinates.
2. **Dishes**: Listings created by Chefs. Contains price, available quantity, and auto-generated nutrition metrics.
3. **Orders**: The transaction record linking a Resident (Customer), a Chef (via Dish), and a Rider. Tracks status transitions (`PENDING` -> `ACCEPTED` -> `PICKED_UP` -> `DELIVERED`).

### Delivery Matching Logic
When a Resident places an order, the system triggers the rider assignment flow:
1. It queries all users with the role `rider` who have toggled their availability to `online`.
2. It calculates the Euclidean distance between the Resident's coordinates and the Rider's coordinates. (Coordinates are randomly assigned upon user registration within a bounded range to simulate a gated community).
3. The order is assigned to the nearest available rider.

### Setup Instructions
1. Clone or download this repository.
2. Open the `index.html` file in any modern web browser (Chrome, Safari, Firefox).
3. No build steps, `npm install`, or local servers are required!

### Testing the End-to-End Flow
1. **Signup as Chef**: Create an account, go to your dashboard, and add a "Dish of the Day". Watch the heuristic AI instantly estimate calories and health score.
2. **Signup as Resident (Customer)**: Open a new tab (or log out), create a resident account. Browse the feed, see the chef's dish, and click "Order".
3. **Signup as Rider**: Open a third tab, create a rider account. Toggle your status to "Online". You will see the incoming order. Accept it, mark it picked up, and then delivered.

## Included Features
- Complete Authentication simulation (Login/Signup with roles).
- Chef Module (Dish creation with heuristic AI nutrition estimation).
- Customer Feed & Ordering.
- Rider availability toggle & Last-mile delivery workflow.
- Responsive, premium dark-mode UI with dynamic interactions.
