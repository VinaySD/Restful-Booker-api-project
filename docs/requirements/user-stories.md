# Product Backlog — Restful-Booker API Test Coverage (v1)

**System Under Test:** Restful-Booker API — `https://restful-booker.herokuapp.com`
**API Docs:** `https://restful-booker.herokuapp.com/apidoc/index.html`
**Prepared by:** Vinay Chaudhari — QA Engineer (API Testing)
**Epic:** Booking API Test Coverage — v1

## Context & Assumptions
Restful-Booker simulates the backend of a hotel's booking system. These requirements are written from the perspective of a fictional hotel's front-desk and operations team consuming this API. There is no UI — requirements are scoped to the API layer only. The API exposes a single authenticated "admin" actor for write operations, so role-based access (front-desk vs. manager) is simplified to one authenticated user for this project.

## Out of Scope
- UI/front-end testing (API-only project)
- Payment processing (not part of this API)
- Multi-user role-based permissions (API only supports one auth level)

---

## User Stories

### US-01 — Authenticate to the system
**Priority:** High | **Estimate:** 3 pts | **Module:** Auth
As a hotel administrator, I want to authenticate with valid credentials so that I can securely manage bookings.
**Acceptance Criteria**
- Valid credentials return a usable token with a success response
- Invalid credentials are rejected, not silently accepted
- A valid token is required before any create/update/delete action succeeds

### US-02 — Create a new booking
**Priority:** High | **Estimate:** 5 pts | **Module:** Booking CRUD
As a front-desk agent, I want to create a new booking with guest and stay details so that a room reservation is recorded.
**Acceptance Criteria**
- Submitting all required fields creates a booking and returns a unique booking ID
- The returned booking data matches what was submitted
- Missing required fields are rejected with a clear response

### US-03 — Retrieve a single booking
**Priority:** Medium | **Estimate:** 2 pts | **Module:** Booking CRUD
As a front-desk agent, I want to look up a booking by its ID so that I can verify or review a reservation.
**Acceptance Criteria**
- A valid booking ID returns the correct booking details
- A non-existent booking ID returns an appropriate "not found" response

### US-04 — Search/filter bookings
**Priority:** Medium | **Estimate:** 3 pts | **Module:** Booking CRUD
As an operations manager, I want to search bookings by guest name or stay dates so that I can find relevant reservations quickly.
**Acceptance Criteria**
- Searching by firstname/lastname returns matching booking IDs
- Searching by checkin/checkout date returns bookings that fall within that range

### US-05 — Update an existing booking (full update)
**Priority:** High | **Estimate:** 5 pts | **Module:** Booking CRUD
As a front-desk agent, I want to update all details of an existing booking so that I can correct or change a reservation.
**Acceptance Criteria**
- An authenticated update with valid data returns the updated record
- An update attempted without a valid token is rejected
- An update with invalid data is rejected, not silently accepted

### US-06 — Update part of a booking (partial update)
**Priority:** Medium | **Estimate:** 3 pts | **Module:** Booking CRUD
As a front-desk agent, I want to update specific fields of a booking without resending the entire record, so that minor corrections are quick and low-risk.
**Acceptance Criteria**
- A partial update changes only the submitted fields
- All other fields remain unchanged
- Requires a valid auth token

### US-07 — Cancel/delete a booking
**Priority:** High | **Estimate:** 3 pts | **Module:** Booking CRUD
As an operations manager, I want to cancel a booking so that it no longer appears as an active reservation.
**Acceptance Criteria**
- An authenticated delete removes the booking
- The deleted booking is no longer retrievable afterward
- Delete attempted without a valid token is rejected

### US-08 — Reject invalid booking data
**Priority:** High | **Estimate:** 5 pts | **Module:** Data Validation
As a QA engineer, I want the API to validate booking data (dates, price, required fields) so that invalid or corrupt data cannot enter the system.
**Acceptance Criteria**
- Invalid date formats are rejected, not silently accepted
- Non-numeric or negative prices are rejected
- Required fields cannot be submitted blank

### US-09 — Confirm service health
**Priority:** Low | **Estimate:** 1 pt | **Module:** System Health
As the operations team, I want a health-check endpoint so that we can confirm the booking service is up and responding.
**Acceptance Criteria**
- The health-check endpoint returns a success response when the service is reachable

---
**Total estimated:** 30 points across 9 stories — to be split across Sprint 1 (Auth + core CRUD) and Sprint 2 (validation, edge cases, regression) during Sprint Planning.
