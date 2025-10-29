[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/yOwut1-r)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=21196702&assignment_repo_type=AssignmentRepo)
# 07
# Neurosynth Frontend (Tailwind + AJAX)

This project provides an interactive AJAX-based web interface for exploring neuroscience meta-analytic data from
https://hpc.psy.ntu.edu.tw:5000
.

The interface is built with Tailwind CSS and vanilla JavaScript (AJAX), and allows users to query the Neurosynth API endpoints for:

available terms,

associated terms with co-occurrence statistics,

and study-level metadata filtered via logical search operators (and, not).

## Features Overview
### 1. Show All Terms Section

Purpose:
Displays all possible keywords available in the Neurosynth database.

Features:

Show all keywords:
Fetches all available terms from the /terms endpoint.

A–Z filter bar:
Interactive alphabetical filter (All, A, B, C, …).
Clicking a letter filters the terms by their starting letter.

Scrollable view:
Results are displayed as keyword badges in a scrollable panel with translucent background.

Endpoint used:

GET https://hpc.psy.ntu.edu.tw:5000/terms

### 2. Associated Terms Section

Purpose:
Given a keyword, shows other terms that commonly co-occur with it,
along with their statistical association measures.

Features:

Dynamic search input:
Input any keyword (e.g., amygdala) and press Search.

Co-occurrence data visualization:
Results are displayed as a sortable table, including:

term — the related word

co_count — co-occurrence frequency

jaccard — Jaccard similarity index

AJAX-based dynamic updates:
Results load instantly without page refresh.

Endpoint used:

GET https://hpc.psy.ntu.edu.tw:5000/terms/<term>


Example:
https://hpc.psy.ntu.edu.tw:5000/terms/amygdala

### 3. Logical Studies Search

Purpose:
Performs a logical keyword search over the Neurosynth studies database and displays
metadata (title, authors, year, journal, etc.) as a table.

Features:

Single flexible input field:
Users can freely enter multi-term queries using logical operators:

amygdala and fear not emotion


Supports unlimited conditions:
There is no restriction on the number of and or not connectors.

Results table:
Displays study metadata including:

id, study_id

year

title

authors

journal

Scrollable table layout:
Automatically adjusts to large datasets with smooth scrolling.

Endpoint used:

GET https://hpc.psy.ntu.edu.tw:5000/query/<query>/studies


Examples:

https://hpc.psy.ntu.edu.tw:5000/query/amygdala/studies

https://hpc.psy.ntu.edu.tw:5000/query/amygdala%20not%20emotion/studies

### 4. History Section

Purpose:
Keeps a record of all previously performed searches and allows quick re-execution.

Features:

Search log:
Every executed search (for terms or studies) is saved with timestamp and query type.

Click-to-replay:
Clicking a past record automatically re-triggers that search using the same query.

Auto-deduplication:
Each unique search (type + query) is stored only once; the most recent replaces older duplicates.

Clear button:
Users can clear the history log manually.

Storage:
Saved locally using localStorage as JSON (neurosearch_history_v1).


## Technical Stack

* Frontend:	HTML5 + Vanilla JS (ES6)
* Styling:	Tailwind CSS via CDN
* Async Logic:	Fetch API with async/await
* Backend API:	Neurosynth API @ NTU
* Local Cache:	Browser LocalStorage for history tracking


## API Endpoints Summary (Endpoint&Description)

* /terms:	List all available keywords
* /terms/<term>	List related / co-occurring terms
* /query/<query>/studies	Search for studies by logical keywords
