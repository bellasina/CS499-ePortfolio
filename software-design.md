# Software Design and Engineering

[← Back to Home](index.md) | [Code Review](code-review.md)

## Grazioso Salvare Rescue Candidate Dashboard

### Artifact Overview

The artifact I selected for the Software Design and Engineering category is my Grazioso Salvare Rescue Candidate Dashboard, which I originally created in February 2026 for CS 340: Advanced Programming Concepts.

The application uses Python, MongoDB, Dash, Pandas, Plotly Express, and Dash Leaflet to work with Austin Animal Center data. Its purpose is to help users review animal records and identify possible candidates for different search-and-rescue categories.

The original project worked, but much of the database access, dashboard layout, filtering logic, callbacks, and visualization behavior were closely connected in one notebook-style implementation. This made the application more difficult to maintain, test, and expand.

---

## Software Design and Engineering Enhancement

For this enhancement, I reorganized the application into a modular structure with separate files for different responsibilities:

- `app.py` handles application startup.
- `config.py` manages configuration settings.
- `database.py` handles database access.
- `services.py` contains reusable application and business logic.
- `layout.py` defines the dashboard interface.
- `callbacks.py` manages the interactive behavior of the application.

Separating these responsibilities made the project easier to understand, maintain, test, and extend.

I also added a search feature that allows users to search by animal name, breed, or animal ID. A Candidate Details section was added so users can view more information about an individual animal after selecting a record.

The map functionality was also improved so records with missing or incomplete location information do not cause the application to fail.

---

## Security and Reliability Improvements

An important part of this enhancement was improving how sensitive database information is handled.

Database credentials are stored in environment variables instead of being placed directly in the Python source files. The private `.env` file is excluded from the submitted project, while an `.env.example` file explains which configuration values are required.

Search input is also handled more safely by escaping user-provided text before it is used in regular-expression searches.

The enhanced application also provides safer error handling so users receive understandable messages instead of unnecessary internal database details.

---

## Skills Demonstrated

This enhancement demonstrates several software engineering skills, including:

- Modular software architecture
- Separation of concerns
- Refactoring existing code
- Reusable functions and services
- Secure configuration management
- Input validation
- Exception and error handling
- User-interface improvement
- Automated testing
- Documentation and maintainability

These changes helped transform the original academic project into a more professional and maintainable application.

---

## Course Outcome Progress

This enhancement supports several CS 499 course outcomes.

The modular architecture supports collaboration because another developer can more easily understand which files are responsible for specific parts of the application.

Professional communication is demonstrated through clear organization, documentation, understandable function names, and user-facing messages.

The project also demonstrates the use of appropriate computing tools and techniques through Python, Dash, MongoDB, PyMongo, Pandas, Plotly, environment variables, and pytest.

Security is demonstrated through environment-based credentials, safer search input, validation, and controlled error messages.

The enhancement also required evaluating design trade-offs. Separating the application into multiple files adds additional project structure, but the benefit is a system that is easier to maintain, test, and expand.

---

## Reflection

One of the most important things I learned from this enhancement is that software can work correctly while still being difficult to maintain.

When I originally created the project, my main goal was to make the dashboard function. During the capstone, I reviewed the project from a software engineering perspective and began considering maintainability, security, testing, and future development.

Breaking the project into smaller modules created a stronger foundation for the later Algorithms and Data Structures and Database enhancements.

I also learned that a working application depends on more than source code. Database configuration, environment variables, external data, testing, and documentation all contribute to whether an application can be maintained and reproduced successfully.

---

## Verification and Testing

The enhanced dashboard was tested using my local MongoDB dataset containing **173,775 animal records**.

I verified that:

- The dashboard successfully loaded the full dataset.
- A specific animal-ID search returned the expected record.
- The Candidate Details section displayed information for a selected animal.
- The Water Rescue filter returned **16,574 matching records**.
- Records without usable map coordinates were handled without causing the application to fail.
- All **8 automated pytest tests passed successfully**.

These results confirmed that the original functionality was preserved while the structure, usability, security, and testability of the application were improved.

---

## Instructor Feedback

My instructor recognized this enhancement as a substantial refactoring of the Grazioso Salvare Dashboard.

The feedback specifically noted the transition from a single notebook-based implementation to a modular application architecture with separate responsibilities for application startup, configuration, database access, services, layout generation, and callback handling.

The instructor also noted that the new structure improved maintainability, readability, scalability, and testability.

Because the feedback supported the design and did not identify corrective issues, I preserved the modular architecture in the final artifact and used it as the foundation for the later enhancements.

---

## Technical Artifacts

[Download the Final Technical Artifact](Angel_Levaomana_CS499_Final_Technical_Artifact.zip)

The technical artifact package contains both the original Grazioso Salvare artifact and the final enhanced artifact used throughout the three CS 499 enhancement categories.

---

## Verification Evidence

The final ePortfolio will also include verification evidence showing the enhanced dashboard and the successful automated test results.
