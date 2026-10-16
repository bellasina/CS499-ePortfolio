# Algorithms and Data Structures

[← Back to Home](index.md) | [Code Review](code-review.md) | [Software Design and Engineering](software-design.md)

## Grazioso Salvare Rescue Candidate Dashboard

### Artifact Overview

For the Algorithms and Data Structures category, I used the same Grazioso Salvare Rescue Candidate Dashboard that I originally created in CS 340: Advanced Programming Concepts.

The application already allowed users to filter animals by rescue category, but the original version treated all matching animals equally. The enhancement added a structured ranking process so the dashboard could identify and prioritize the strongest rescue candidates instead of only displaying filtered results.

---

## Algorithms and Data Structures Enhancement

The main improvement was the addition of a rescue-candidate scoring and ranking system.

I created a centralized `RESCUE_PROFILES` dictionary that stores the rules for each rescue category. These rules include preferred breeds and age ranges.

The `score_candidate()` function evaluates each animal using the selected rescue category and assigns a suitability score based on factors such as:

- Animal type
- Preferred breed match
- Preferred age range

A candidate can receive up to:

- 20 points for being a dog
- 50 points for matching a preferred breed
- 30 points for being within the preferred age range

The scoring function also produces a "Why Ranked" explanation so the user can understand how the score was calculated.

---

## Priority Queue and Ranking Algorithm

After each candidate receives a score, the application uses a bounded min-heap implemented with Python's `heapq` module.

The heap keeps only the strongest top-k candidates instead of sorting every matching animal.

For n records and a top-k request, the main ranking process has approximately:

**O(n log k) time complexity**

and requires:

**O(k) additional space**

This approach is useful because the dashboard only needs to display a limited number of the strongest candidates instead of ordering the entire dataset.

---

## User Interface Integration

The ranking algorithm is integrated directly into the dashboard.

The **Top Rescue Candidates** table displays:

- Rank
- Suitability Score
- Animal ID
- Name
- Breed
- Age
- Why Ranked

The ranking results update when the rescue category or search criteria change.

This enhancement transformed the dashboard from a simple filtering tool into a decision-support system that can prioritize the strongest matching animals.

---

## Skills Demonstrated

This enhancement demonstrates several algorithm and data-structure skills, including:

- Dictionaries for organizing scoring rules
- Weighted scoring algorithms
- Priority queues
- Bounded min-heaps
- Top-k ranking
- Time complexity analysis
- Space complexity analysis
- Input validation
- Edge-case handling
- Deterministic tie breaking
- Automated testing

---

## Course Outcome Progress

This enhancement strongly demonstrates the course outcome related to designing and evaluating computing solutions using algorithmic principles and appropriate computer science practices.

I had to break the ranking problem into smaller parts, including defining scoring rules, converting age information, calculating scores, maintaining the strongest candidates, handling ties, and presenting results clearly.

I also evaluated the trade-off between sorting every matching record and using a bounded heap.

The bounded heap is a better fit for the dashboard because only a small number of top candidates need to be displayed.

The enhancement also demonstrates professional communication through the "Why Ranked" explanations and project documentation.

---

## Reflection

One of the most important things I learned from this enhancement is that choosing a data structure should depend on what the program actually needs to accomplish.

A full sort would have worked, but it would have done more work than necessary when the dashboard only needed a small list of the strongest candidates.

Using a bounded min-heap helped me better understand how input size, requested output size, execution time, and memory usage are connected.

I also learned the importance of separating the scoring rules from the ranking algorithm. Keeping the rescue profiles in dictionaries made the logic easier to read, maintain, and update.

Another challenge involved inconsistent real-world data. Some animal ages were represented differently or were missing. I added helper logic to normalize age information and safely handle missing values.

I also added deterministic tie-breaking logic so candidates with identical scores could still be ranked consistently without causing errors.

---

## Verification and Testing

The automated test suite was expanded from 8 tests to **16 tests** for this enhancement.

The tests verify:

- Age conversion
- Numeric age handling
- Rescue-profile scoring
- Missing-age behavior
- Top-k ranking order
- Deterministic ties
- Malformed-record handling
- Rescue-type validation
- Invalid k values

All **16 automated tests passed successfully**.

I also verified the ranking feature through the running dashboard using the local MongoDB dataset.

The application successfully produced ranked candidate lists for:

- Water Rescue
- Mountain/Wilderness Rescue
- Disaster/Individual Tracking

This confirmed that the algorithm worked both in automated tests and in the actual dashboard interface.

---

## Instructor Feedback

My instructor recognized the use of the centralized rescue-profile dictionary, weighted candidate scoring, and bounded min-heap as strong algorithm and data-structure choices.

The feedback also noted that the ranking process improved scalability and efficiency and moved the application beyond simple filtering.

Because the instructor feedback supported the technical approach and did not identify corrective issues, I preserved the core scoring and ranking design in the final artifact.

---

## Verification Evidence

The dashboard verification showed:

- Water Rescue selected
- 16,574 matching records
- Top 10 ranked rescue candidates
- Suitability scores
- "Why Ranked" explanations

The automated pytest verification also showed:

**16 passed**

---

## Technical Artifacts

[Download the Final Technical Artifact](Angel_Levaomana_CS499_Final_Technical_Artifact.zip)

The technical artifact package contains both the original Grazioso Salvare artifact and the final enhanced artifact used throughout the three CS 499 enhancement categories.
