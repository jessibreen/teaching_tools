# Teaching Tools

Utilities for importing Canvas textbox submissions into an Obsidian
grading vault.

These tools automate:

-   creating one folder per student into an Obsidian vault
-   converting Canvas HTML textbox submissions to Markdown
-   placing each submission into the correct student folder in the vault

This allows tracking student projects in Obsidian without manual file handling.

------------------------------------------------------------------------

# Initial Setup

## 1. Clone repo

## 2. Create virtual environment

    python3 -m venv .venv
    source .venv/bin/activate

## 3. Install dependencies

    pip install -r requirements.txt

------------------------------------------------------------------------

# Start of semester: Create student folders

This only needs to be done **once per semester**.

## Export roster from Eagle Access for each class or section

Save file as:

    roster.csv

Roster format:

    "Student Name"
    lastname, firstname

------------------------------------------------------------------------

## Run folder creation tool

    python student_folders.py roster.csv -o StudentVault

Where:

-   `roster.csv` = Class roster export
-   `StudentVault` = Obsidian vault for the semester

------------------------------------------------------------------------

## Result

Creates:

    StudentVault/

    firstname_lastname/
    firstname_lastname/
    firstname_lastname/

------------------------------------------------------------------------

# Each assignment: Import Canvas textbox submissions

This is run **once per assignment**.

------------------------------------------------------------------------

## Export submissions from Canvas

For textbox assignments:

Download submission HTML files.

Place in folder:

    submissions/

------------------------------------------------------------------------

## Run import tool

    python html2md.py submissions_folder \
      --vault-root StudentVault \
      --note-name assignment_name.md

------------------------------------------------------------------------

## Result

Each student folder receives:

    firstname_lastname/

    assignment_name.md

File contains:

    # Submission

    (student work)

    ---

    # Feedback

    (write feedback here)

------------------------------------------------------------------------

# Typical use (quick reference)

Start semester:

    python student_folders.py roster.csv -o StudentVault

Each assignment:

    python html2md.py submission_folder \
      --vault-root StudentVault \
      --note-name assignment_name.md
