# Databases

[← Back to Home](index.md) | [Code Review](code-review.md) | [Software Design and Engineering](software-design.md) | [Algorithms and Data Structures](algorithms-data-structures.md)

## Grazioso Salvare Rescue Candidate Dashboard

### Artifact Overview

For the Databases category, I used the same Grazioso Salvare Rescue Candidate Dashboard that I originally created in CS 340: Advanced Programming Concepts.

The original project already connected to MongoDB and included basic create, read, update, and delete methods. However, the dashboard mainly used the database to retrieve information.

For this enhancement, I expanded the database layer so the application could validate data, manage records safely, improve query performance, summarize information through aggregation, and handle database operations more securely.

---

## Database Enhancement

One of the main improvements was the addition of stronger record validation.

The enhanced `database.py` includes validation that:

- Requires important fields for new records
- Trims and validates text values
- Checks latitude and longitude ranges
- Rejects unsupported fields
- Supports partial updates
- Validates MongoDB ObjectIds before update or delete operations

These checks reduce the chance that invalid or unintended information will be stored in the database.

---

## Safer Update and Delete Operations

The original CRUD implementation used broad `update_many()` and `delete_many()` operations.

For the enhanced dashboard, I changed this behavior so updates and deletions target one exact MongoDB document.

Each selected record keeps its MongoDB `_id` as a safe `record_id`, and the repository uses:

- `update_one()`
- `delete_one()`

with the correct ObjectId.

This reduces the risk of accidentally changing or deleting multiple records.

The dashboard also requires confirmation before a selected record is deleted.

---

## Indexing and Query Performance

The enhanced database layer creates or verifies indexes on fields commonly used by the dashboard, including:

- `animal_id`
- `name`
- `outcome_type`
- `animal_type` and `breed`

I also added an exact animal-ID search path so animal IDs can use equality matching instead of relying only on regular-expression searches.

This enhancement helped me understand the trade-off involved with indexing. Indexes can improve repeated searches, but they also add work when records are inserted or updated. Because of this, I selected indexes based on the dashboard's normal workload instead of indexing every field.

---

## MongoDB Aggregation

I added a database-backed summary using MongoDB's aggregation framework.

The `aggregate_breed_summary()` method uses stages that:

- Match the current search and filter criteria
- Group records by animal type and breed
- Count matching records
- Sort the results
- Limit the number of results
- Return only the fields needed by the dashboard

This allows MongoDB to perform useful data processing before sending the results back to Python.

The aggregation results are displayed in the dashboard as a summary table and visualization.

---

## Dashboard CRUD Integration

Create, update, and delete functionality was connected directly to the Dash interface.

The user can:

- Select a record
- Load it into the management form
- Create a new record
- Update the selected record
- Delete a selected record after confirmation

After a successful database change, the dashboard refreshes its information so the user sees current results instead of stale data.

This includes refreshing the main table, ranking information, and database summary.

---

## Security and Data Integrity

The earlier security improvements were preserved throughout this enhancement.

Database usernames and passwords are stored in environment variables rather than directly in the Python files.

The real `.env` file is excluded from the public project.

The application also avoids displaying raw database exceptions to users. Instead, database failures are translated into safer and more understandable messages.

Together, these improvements support both database security and data integrity.

---

## Skills Demonstrated

This enhancement demonstrates several database development skills, including:

- MongoDB CRUD operations
- PyMongo
- Record validation
- ObjectId validation
- Exact-document targeting
- Index creation and management
- Query optimization
- Aggregation pipelines
- Data integrity
- Secure configuration management
- Database error handling
- User-interface and database integration
- Automated testing

---

## Course Outcome Progress

This enhancement supports several CS 499 course outcomes.

Professional communication is demonstrated through understandable user messages, documentation, and clearly organized database behavior.

The enhancement also required evaluating design trade-offs, such as selecting useful indexes without indexing every field and choosing exact single-record operations instead of broad multi-record updates and deletions.

Industry-relevant tools and techniques are demonstrated through MongoDB, PyMongo, ObjectIds, indexes, aggregation pipelines, Dash callbacks, automated testing, and environment-based configuration.

Security is demonstrated through validation, allow-listed fields, protected credentials, safe error handling, exact-record targeting, and delete confirmation.

---

## Reflection

One of the biggest lessons I learned from this enhancement is that having CRUD methods does not automatically make a database feature complete or safe.

The original application technically supported create, read, update, and delete operations, but reviewing the project during the capstone showed that those operations could be improved significantly.

I began thinking about database operations from the user's perspective:

- What happens if required information is missing?
- How can the application identify one exact record?
- What happens if a user accidentally selects delete?
- How should the interface respond after the database changes?

These questions helped me design a more reliable database layer.

I also learned more about the difference between the Austin Animal Center `animal_id` and MongoDB's unique `_id` field. Using the MongoDB document ID made it possible to safely target one exact document for updates and deletions.

Another important lesson came from using aggregation. Earlier versions of the project mainly retrieved information and processed it in Python or Pandas. The aggregation enhancement showed me that MongoDB can perform useful grouping, counting, sorting, and summarization before data reaches the application.

---

## Verification and Testing

The automated test suite was expanded from 16 tests to **30 tests** for this enhancement.

The tests verify:

- Required create fields
- Text validation
- Coordinate validation
- Unsupported-field rejection
- Partial updates
- ObjectId validation
- Index definitions
- Create behavior
- Exact-record updates
- Exact-record deletion
- Aggregation pipeline stages
- Safe database error handling

All **30 automated tests passed successfully**.

I also ran Python syntax compilation checks on:

- `app.py`
- `callbacks.py`
- `config.py`
- `database.py`
- `layout.py`
- `services.py`

All files compiled successfully.

---

## Instructor Feedback

My instructor described this database enhancement as comprehensive and well executed.

The feedback specifically recognized the improvements in:

- Validation
- Reliability
- Data integrity
- Indexing
- Query performance
- MongoDB aggregation
- Exact ObjectId targeting
- Controlled CRUD operations
- Security-conscious development
- Application integration

The instructor also noted that the dashboard successfully connected create, update, delete, aggregation, ranking, and refresh operations to the underlying database layer.

Because the feedback confirmed that the enhancement was complete and did not identify corrective issues, I preserved the database design in the final artifact.

---

## Technical Artifacts

**Original Artifact:** Link will be added after the original code is uploaded.

**Enhanced Artifact:** Link will be added after the enhanced code is uploaded.
