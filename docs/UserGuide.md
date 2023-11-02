---
layout: page
title: User Guide
---

# Table of Contents

- [Introduction](#introduction)
- [Quick Start](#quick-start)
- [GUI Summary](#gui-summary)
- [Features](#features)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Known Issues](#known-issues)
- [Command Summary](#command-summary)
  - [General Command](#general-command)
  - [Application Management Command](#applicant-management-command)
  - [Interview Management Command](#interview-management-command)
- [Glossary](#glossary)

--------------------------------------------------------------------------------------------------------------------

# Introduction

Tired of sending out offers to the best candidates, just to receive a disappointing reply that they have already accepted another offer that was sent out before yours?

**InterviewHub**  is a desktop app for engineering manager to schedule job interviews and manage applicants.
By optimizing recruitment workflows, we enable faster decision-making, helping you secure top talent before your competitors.

It is optimized for use via a **Command Line Interface** (CLI) while still having the benefits of a **Graphical User Interface** (GUI).
If you can type fast, **InterviewHub** can get your Interview management tasks done faster than traditional GUI apps.

What are you waiting for? Let's get started using **InterviewHub** by following the [Quick Start](#quick-start) section!

--------------------------------------------------------------------------------------------------------------------

# Quick Start

1. Ensure you have Java `11` or above installed in your Computer.

2. Download the latest `InterviewHub.jar` from [here](https://github.com/AY2324S1-CS2103T-T11-2/tp/releases).

3. Copy the file to the folder you want to use as the home folder for InterviewHub.

4. Double-click the file to start the app. The Graphical User Interface(GUI) should appear in a few seconds.

5. To get a better understanding of what you see. Please refer to the [GUI Summary](#gui-summary) for more details.

--------------------------------------------------------------------------------------------------------------------

# GUI Summary

![GUI Summary](images/GuiSummary.png)

For each applicant and each interview, we see the following details:

| Applicant | Interview  |
|-----------|------------|
| Name      | Job role   |
 | Tags      | Start time |
| Phone     | End time   |
| Address   | Rating     |
 | Email     |            |

--------------------------------------------------------------------------------------------------------------------
# Features

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g. `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit`, `nuke` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

## Viewing help : `help`

Shows a message explaining how to access the help page.

![help message](images/helpMessage.png)

Format: `help`

## Adding an applicant: `add-a`

Adds an applicant to the address book.

Format: `add-a n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]`

Examples:
* `add-a n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/friend t/colleague`

## Adding an interview: `add-i`

Adds an interview to the address book.

Format: `add-i app/APPLICANT_ID jr/JOB_ROLE start/START_DATE_AND_TIME end/END_DATE_AND_TIME`

:information_source: JOB_ROLE allows empty strings to be entered to handle situations where the applicant is applying
to the company in general.

* List of accepted date formats:
  * Day and time: 
    * `Tue 1600`
    * `Tue 4.00pm`
    * `Tue 4pm`
  * DD/MM/YYYY and time:
    * `16 May 2024 1515`
    * `16 May 2024 3.15pm`
    * `16 May 2024 3pm`
    * `16-05-2024 1515`
    * `16-05-2024 3.15pm`
    * `16-05-2024 3pm`
    * `16-05-24 1515`
    * `16-05-24 3.15pm`
    * `16-05-24 3pm`
    * `16/05/2024 1515`
    * `16/05/2024 3.15pm`
    * `16/05/2024 3pm`
    * `16/05/24 1515`
    * `16/05/24 3.15pm`
    * `16/05/24 3pm`
  * MM, DD and time:
    * `16 May 1515`
    * `16 May 3.15pm`
    * `16 May 3pm`
    * `16 January 1515`
    * `16 January 3.15pm`
    * `16 January 3pm`
    * `16/5 1515`
    * `16/5 3.15pm`
    * `16/5 3pm`
    * `16/05 1515`
    * `16/05 3.15pm`
    * `16/05 3pm`

* Expected outputs:
  * When the user enters the date properly: `added <interview description> at <time>`
  * When the applicant index provided is invalid: `The applicant index provided is invalid`
  * When the user does not input a valid date: `“Please specify a valid date!”`
  * When the user inputs a valid date without a time: `"Please enter an interview time!"`
  * When the user enters a valid date in the past: `<todo>`
  * When there is an interview clash: `“Oops! You have an <insert interview object> scheduled at <from date & by date>`

Examples:
* `add-i app/3 jr/software engineer start/11-12-2023 1400 end/11-12-2023 1500`

## Listing all applicants : `list-a`

Shows a list of all applicants in the address book onto the GUI.

Format: `list-a`

## Listing all interviews : `list-i`

Shows a list of all interviews in the address book onto the GUI.

Format: `list-i`

## Editing an applicant : `edit-a`

Edits an existing applicant in the address book.

Format: `edit-a APPLICANT_INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS]`

* Edits the person at the specified `APPLICANT_INDEX`. The index refers to the index number shown in the displayed applicant list.
* The index **must be a positive integer** 1, 2, 3, …​ The upper limit of valid integers is the number of applicants currently displayed in the applicant list
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.

Examples:
*  `edit-a 1 n/John Doe` Edits the name of the 1st applicant to be `John Doe`.
*  `edit-a 2 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the 2nd applicant to be `91234567` and `johndoe@example.com` respectively

## Editing an interview : `edit-i`

Edit an existing interview in the address book.

Format: `edit-i INTERVIEW_INDEX [app/APPLICANT_ID] [jr/JOB_TITLE] [start/START_DATE_AND_TIME] [end/END_DATE_AND_TIME]`

* Edits the interview at the specified `INTERVIEW_INDEX`. The index refers to the index number shown in the displayed interview list.
* The index **must be a positive integer** 1, 2, 3, …​ The upper limit of valid integers is the number of interviews currently displayed in the interview list
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.

Examples:
*  `edit-i 1 jr/software-engineer` Edits the job title of the 1st interview to be `software-engineer`.
*  `edit-i 2 jr/data-analyst` Edits the job title of the 2nd interview to be `data-analyst`.

## Deleting an applicant : `delete-a`

Deletes the specified applicant from the address book.

Format: `delete-a INDEX`

* Deletes the applicant at the specified `INDEX`.
* The index refers to the index number shown in the displayed applicant list.
* The index **must be a positive integer** 1, 2, 3, …​ The upper limit of valid integers is the number of applicants currently displayed in the applicant list

Examples:
* `delete-a 1` deletes the 1st applicant in the address book.

## Deleting an interview : `delete-i`

Deletes the specified interview from the address book.

Format: `delete-i INDEX`

* Deletes the interview at the specified `INDEX`.
* The index refers to the index number shown in the displayed interview list.
* The index **must be a positive integer** 1, 2, 3, …​ The upper limit of valid integers is the number of interviews currently displayed in the interview list

Examples:
* `delete-i 1` deletes the 1st interview in the address book.

## Finding applicants: `find-a`

Finds applicants whose attributes contain any of the given keywords.

Format: ``find-a [n/KEYWORDS [MORE_KEYWORDS]...] [p/NUMBER]
[e/KEYWORDS [MORE_KEYWORDS]...] [a/KEYWORDS [MORE_KEYWORDS]...] [t/KEYWORDS [MORE_KEYWORDS]...]``

* The search is case-insensitive. e.g. `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* At least one of the optional fields must be provided
* Any of the fields (name, phone, email, address, tags) can be searched
* Only full words will be matched e.g. `Han` will not match `Hans` for name, address and tags
* For phone, partial numbers will match e.g. `987` will match `98765432`
* Applicants matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find-a n/John` returns `john` and `John Doe`
* `find-a n/alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find-a n/alex david'](images/findAlexDavidResult.png)
* `find-a p/874 a/serangoon ang` returns `97438807`, `Serangoon Gardens`,
`Serangoon Gardens Street`, `Ang Mo Kio`<br>
  ![result for 'find-a p/874 a/serangoon ang'](images/findPhoneAddress.png)

## Finding interview by job title: `find-i`

Find interviews which jobs title contain any of the given keywords.

Format: `find-i KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g. `ANALYST` will match `analyst`
* The order of the keywords does not matter. e.g. `Software Engineer` will match `Engineer Software`
* Only the job title is searched.
* Only full words will be matched e.g. `Analyst` will not match `Analysts`
* Applicants matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Software Engineer` will return `Software-Developer`, `System-Engineer`

Examples:
* `find-i software data` returns `Software-Engineer` and `Data-Analyst`.

## Rating an interview: `rate`

Rate the specified interview in the address book.

Format: `rate INDEX RATING`

* Rates the interview at the specified `INDEX`.
* The index refers to the index number shown in the displayed interview list.
* The index **must be a positive integer** 1, 2, 3, …​ The upper limit of valid integers is the number of interviews currently displayed in the interview list
* The `RATING` must be a non-negative one decimal place number between 0.0 to 5.0 inclusive.

Examples:
* `rate 1 3.0` rates the first interview with a rating of 3.0.

## Sorting interviews by rating: `sort-rate`

Sort the interview list by rating in descending order (highest to the lowest rating).

Format: `sort-rate`

## Exiting the program : `exit`

Exits the program.

Format: `exit`

## Clearing all applicants and interviews : `clear`

Clears all applicants and interviews from the address book.

Format: `clear`

## Saving the data

InterviewHub data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

## Editing the data file

InterviewHub data are saved automatically as a JSON file `[JAR file location]/data/interviewhub.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, InterviewHub will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.
</div>

--------------------------------------------------------------------------------------------------------------------

# Frequently Asked Questions

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous InterviewHub home folder.

--------------------------------------------------------------------------------------------------------------------

# Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.

--------------------------------------------------------------------------------------------------------------------

# Command Summary

## General Command

| Action                                  | Format, Examples |
|-----------------------------------------|------------------|
| **Clear all applicants and interviews** | `clear`          |
| **Help**                                | `help`           |
| **Exit**                                | `exit`           |

## Applicant Management Command

| Action                   | Format, Examples                                                                                                                                                                                                 |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Add applicant**        | `add-a n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/friend t/colleague`                                            |
| **Delete applicant**     | `delete-a APPLICANT_INDEX`<br> e.g., `delete-a 3`                                                                                                                                                                |
| **Edit applicant**       | `edit-a APPLICANT_INDEX [n/NAME] [t/INTERVIEW_DATETIME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS]`<br> e.g.,`edit-a 2 n/John Doe`                                                                                   |
| **Find applicant**       | `find-a [n/KEYWORDS [MORE_KEYWORDS]...] [p/NUMBER] [e/KEYWORDS [MORE_KEYWORDS]...] [a/KEYWORDS [MORE_KEYWORDS]...] [t/KEYWORDS [MORE_KEYWORDS]...]` <br> e.g., `find-a n/John Bob p/98765432 e/John@example.com` |
| **List applicants**      | `list-a`                                                                                                                                                                                                         |

## Interview Management Command

| Action                        | Format, Examples                                                                                                                      |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Add interview**             | `add-i app/APPLICANT_INDEX jr/JOB_TITLE time/INTERVIEW_DATETIME` <br> e.g., `add-i app/18 jr/software engineer time/2022-12-12 18:00` |
| **Delete interview**          | `delete-i INTERVIEW_INDEX`<br> e.g., `delete-i 3`                                                                                     |
| **Edit interview**            | `edit-i INTERVIEW_INDEX [app/APPLICANT_INDEX] [jr/JOB_TITLE] [time/INTERVIEW_DATETIME]`<br> e.g.,`edit-i 2 jr/software-engineer`      |
| **Find interview by job**     | `find-i KEYWORD [MORE_KEYWORDS]`<br> e.g., `find-i software-engineer`                                                                 |
| **List interview**            | `list-i`                                                                                                                              |
| **List free time**            | `list-freetime INTERVIEW_DATETIME` <br> e.g, `list-freetime 12-12-2024`                                                               |
| **List interview for today**  | `list-i-today`                                                                                                                        |
| **Mark interview as done**    | `mark INTERVIEW_INDEX` <br> e.g., `mark 3`                                                                                            |
| **Rate interview**            | `rate INTERVIEW_INDEX RATING` <br> e.g., `rate 1 3.0`                                                                                 |
| **Show completed interview**  | `show-done`                                                                                                                           |
| **Show incomplete interview** | `show-undone`                                                                                                                         |
| **Sort interview by rating**  | `sort-rate`                                                                                                                           |
| **Sort interview by time**    | `sort-time`                                                                                                                           |

--------------------------------------------------------------------------------------------------------------------

# Glossary

TBD
