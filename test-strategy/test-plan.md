# Test Plan — Restful-Booker API Test Coverage (v1)

**Project:** Restful-Booker API Testing
**Prepared by:** Vinay Chaudhari — QA Engineer (API Testing)
**System Under Test:** `https://restful-booker.herokuapp.com`
**Reference:** Product Backlog — `docs/01-requirements/user-stories.md`

## 1. Objective
Validate the functional correctness, data validation, and authentication behavior of the Restful-Booker Booking API across 2 Agile sprints, covering requirements, design, execution, defects, regression, and closure.

## 2. Scope

**In scope**
- Authentication (`POST /auth`)
- Booking CRUD: Create, Get (single + filtered list), full Update, partial Update, Delete
- Data validation (required fields, date formats, price values)
- Health check (`GET /ping`)
- Functional, negative, boundary, and basic auth-state testing

**Out of scope**
- Load/performance testing (beyond basic response-time sanity checks)
- Security penetration testing (only lightweight negative-input checks are included)
- UI testing (API-only project, no front end exists)

## 3. Test Approach
Agile/Scrum, 2 one-week sprints:
- **Before Sprint 1 (planning):** requirements, test plan, test design, environment and test data setup
- **Sprint 1:** execute and log defects for US-01 to US-04 and US-09 (auth, create, get, search, health)
- **Sprint 2:** execute and log defects for US-05 to US-08 and NFR-01 (update, partial update, delete, validation, response time, end-to-end flow), retest Sprint 1 defects, run full regression, closure

Testing is primarily manual (executed in Postman), with the Collection Runner used for data-driven cases. Newman/CI automation is an optional stretch item after core execution is complete.

## 4. Test Types
| Type | Purpose |
|---|---|
| Functional | Confirm each endpoint behaves per its documented contract |
| Negative | Invalid/missing/malformed input is rejected correctly |
| Boundary | Edge values (empty strings, min/max price, long strings) |
| Auth-state | Valid / missing / invalid token behavior on protected endpoints |
| Regression | Re-run of the full pack in Sprint 2, before closure |

## 5. Environment & Tools
| Tool | Use |
|---|---|
| Postman | Test design & manual execution |
| Postman Environment | Holds `baseUrl` and `token` variables |
| Newman (optional) | CLI execution for CI |
| Jira | Requirement/story tracking, defect lifecycle, sprint board |
| GitHub | Version control for all test artifacts and the Postman collection |
| Excel/Sheets | Test scenarios, test cases, RTM |

Only one real environment exists (the public sandbox), so there's no Dev/QA/Prod separation for this project.

## 6. Roles & Responsibilities
Solo project — Vinay owns test planning, design, execution, defect management, and reporting. In a real team, requirement authoring would normally sit with a BA/PO and defect triage would involve a dev lead.

## 7. Entry Criteria (before execution starts)
- User stories reviewed
- Test scenarios and test cases written and peer-reviewable
- Postman collection and environment ready
- Jira project and board set up

## 8. Exit Criteria (before closure)
- All planned test cases executed
- No open Critical/High severity defects (or explicitly deferred with reason)
- All logged defects retested and closed or documented as known issues
- Test Summary Report completed

## 9. Defect Classification
| Severity | Meaning |
|---|---|
| Critical | Core function broken, no workaround (e.g., cannot create a booking) |
| High | Major functional or data-integrity issue |
| Medium | Incorrect behavior with a workaround, or contract inconsistency |
| Low | Cosmetic or minor semantic issue (e.g., wrong status code on success) |

| Priority | Meaning |
|---|---|
| P1 | Fix before proceeding |
| P2 | Fix this sprint |
| P3 | Fix if time allows |
| P4 | Track, no immediate action needed |

Restful-Booker is a third-party sandbox, so the project team cannot fix its defects. Each defect is logged with evidence, re-run in Sprint 2 to confirm it still reproduces, and then closed as Won't Fix (external) with the observed behaviour documented.

## 10. Risks & Mitigations
| Risk | Mitigation |
|---|---|
| Sandbox API resets its data periodically | Every test case creates its own prerequisite data — no test depends on data surviving between runs |
| Shared public API may have variable response times | Response-time assertions use a generous threshold (e.g., under 3s), not strict production SLAs |
| Single environment only | Documented here as a known constraint of using a shared public sandbox |

## 11. Deliverables
Requirements → Test Scenarios & Cases → RTM → Postman Collection/Environment/Test Data → Execution Reports (per sprint) → Defect Log → Regression Summary → Test Summary Report → Interview-Prep Guide. (Full paths in the repo README.)

## 12. Schedule
| Sprint | Focus | Output |
|---|---|---|
| Planning | Requirements, plan, test design, environment and data | Docs, test cases, Postman collection |
| Sprint 1 (Week 1) | US-01 to US-04, US-09 | Execution report, defect log |
| Sprint 2 (Week 2) | US-05 to US-08, NFR-01, retest, regression | Regression summary, closure report |
