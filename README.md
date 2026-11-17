# README.md

The Spectrum (Gradient): Detailed Design
1. Core concept

Each day, players see 8 items (words, images, or both) that look unrelated. They are all positioned on one hidden scale. The player drags them into the order they believe runs from lowest to highest. The axis is revealed only after the final guess, or progressively through hints.

2. Daily loop
Open: today’s puzzle number and a “?” where the axis name would be.
Arrange: drag the 8 cards into slots 1–8. Ends are labelled only “Lowest” and “Highest”.
Submit: the player gets feedback (see section 4).
Iterate: they have a limited number of attempts (default 5).
Reveal: the axis, each item’s true value, and a one-line fun fact per item.
Share: a spoiler-free emoji grid, plus streak and stats update.
3. Puzzle anatomy
Field	Notes
Axis	e.g. “Year of invention”, with unit and direction (ascending/descending)
Items (8)	Each has a label, an optional image, a true value, and a source URL
Display value	Formatted for the reveal (“1876”, “2.2M SHU”, “4 syllables”)
Difficulty	1–5, set by editors and later calibrated by real solve data
Hint 1	Category of axis (“A date”, “A quantity”, “A linguistic property”)
Hint 2	Reveals the axis name
Hint 3	Locks the lowest and highest items in place
Fun facts	One line per item, shown on reveal

Axis categories (for scheduling variety): time/dates, physical measures (height, weight, distance, temperature), counts (population, syllables, letters), money, speed, intensity (Scoville, Mohs hardness, decibels), ranks and ratings, and “weird” axes (Scrabble score, alphabet position, Wikipedia page length).

Content rules

All 8 values must be distinct and unambiguously ordered, with a minimum gap so no two items are effectively tied.
Every value needs a verifiable source.
No more than 2 of the 8 items may be a “giveaway” that makes the axis obvious.
Avoid repeating the same axis within 30 days, and avoid the same category more than 2 days in a row.
Mix item formats: text only, image only, or mixed. Images need alt text.
4. Feedback and scoring

Feedback after each submit (pick one model and keep it consistent):

Position feedback (recommended): green when a card is in its exact slot, yellow when it is within 1 slot, grey otherwise. This is Wordle-like and gives deduction without revealing the axis.
Alternative: show only the count of correct positions. This is harder and encourages more thought.

Score (0–100)

Base score = 100 minus the sum of positional errors, normalised.
Attempt multiplier: 1st try = ×1.0, 2nd = ×0.85, 3rd = ×0.7, and so on.
Hint penalty: −10 per hint used.
A perfect solve on the first try with no hints earns a “Spectrum Master” badge.

Share string example

The Spectrum #214 — 3/5 🌈
🟩🟨⬜🟩🟩⬜🟨🟩
🟩🟩⬜🟩🟩🟨🟩🟩
🟩🟩🟩🟩🟩🟩🟩🟩
5. Progression and retention
Streaks with a weekly “freeze” token.
Stats page: win rate, average attempts, guess distribution, best axis category.
Archive: past puzzles are playable, with streaks unaffected.
Achievements: “No hints for 7 days”, “Solved a Scoville day”, “Perfect Friday”.
Weekly themed axes: for example, Fridays are “Food & Drink”, with optional themed packs later.
Leaderboard (optional, later): friends-only to keep it low-pressure.
6. UX details
Drag-and-drop with a tap-to-swap fallback for accessibility.
Slot labels show only “1 (lowest)” and “8 (highest)”.
Colour-blind-safe palette, with icons or patterns in addition to colour.
Full keyboard support and screen-reader labels.
Dark and light modes, with large touch targets for mobile.
Reveal animation: cards sort themselves and count up to their true values.
Optional “Spectrum bar” visual: a gradient strip that highlights where each card actually sits.
7. Technical architecture
Frontend: a responsive web app (PWA), with local storage for guest play.
Backend: a puzzle service with a daily puzzle endpoint (served by UTC date or local date, a decision to make), a submit/validate endpoint (answers never sent to the client before solve or final attempt), and stats sync.
Data: puzzles in a database plus an admin tool, with a scheduling calendar and a validation pipeline.
Anti-cheat: server-side validation, with the answer key delivered only on completion or when attempts run out.
Analytics: solve rates, hint usage, and drop-off per puzzle, used to recalibrate difficulty.
8. Content pipeline
An editor tool for creating puzzles, with automatic checks for distinct values, minimum gaps, source URL present, and axis repeat rules.
A review state machine: Draft → Review → Approved → Scheduled → Published.
A 14-day content buffer alert if fewer than 14 approved puzzles are scheduled.
Community submission form (later), feeding the same review pipeline.
9. Example puzzles
Year of invention: telephone, microwave oven, zip, printing press, LED, GPS, Post-it note, bicycle.
Number of syllables: “onomatopoeia”, “cat”, “elephant”, “refrigerator”, “banana”, and others.
Scoville heat: bell pepper, jalapeño, cayenne, habanero, ghost pepper, Carolina Reaper, and others.
Mohs hardness: talc, gypsum, calcite, fluorite, apatite, quartz, topaz, diamond.
10. Milestones
MVP: core play loop, 30 seeded puzzles, position feedback, share string, local stats.
v1: accounts, streaks, archive, hints, admin tool.
v1.5: achievements, themed weeks, analytics-driven difficulty.
v2: community submissions, friend leaderboards, daily notification.
11. Open questions
One global puzzle time (UTC) versus each player’s local midnight?
Do you want 5 attempts, or unlimited with a score penalty?
Text-only at launch, or images from day one (licensing and sourcing)?
Is an ascending/descending direction ever shown, or always lowest to highest?
