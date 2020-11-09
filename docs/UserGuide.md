---
layout: page
title: User Guide
---

SWEe! is a  **desktop app for CS2103T students to manage their learning progress mainly through flashcards**. It is optimized for CLI users so that frequent tasks can be done faster by typing in commands. If you can type fast, SWEe! can create your CS2103T flashcards faster than traditional GUI apps.


* Table of Contents
    - [Quick start](#quick-start)
    - [Application layout](#application-layout)
    - [Notes about the command format](#notes-about-the-command-format)
    - [Common Input Fields](#common-input-fields)
    - [Features](#features)
        - [Add a flashcard](#add-a-flashcard--add): `add`
        - [Clear all flashcards](#clear-all-flashcards--clear): `clear`
        - [Delete a flashcard](#delete-a-flashcard---delete): `delete`
        - [Edit a flashcard](#edit-a-flashcard---edit): `edit`
        - [Filter for flashcards](#filter-for-flashcards---filter): `filter`
        - [Favourite a flashcard](#favourite-a-flashcard---fav) : `fav`
        - [Unfavourite a flashcard](#unfavourite-a-flashcard---unfav): `unfav`
        - [Find flashcards](#find-flashcards--find): `find`
        - [View help](#view-help--help): `help`
        - [List all flashcards](#list-all-flashcards--list): `list`
        - [Review flashcards](#review-flashcards-review) : `review`
        - [Quiz flashcards](#quiz-flashcards-quiz): `quiz`
        - [Sort all flashcards](#sort-all-flashcards--sort): `sort`
        - [View a flashcard](#view-a-flashcard---view): `view`
        - [View the statistics of a flashcard](#view-the-statistics-of-flashcard--stats): `stats`
        - [Exit the program](#exit-the-program--exit): `exit`
        - [Saving the data](#saving-the-data)
    - [FAQ](#faq)
    - [Command summary](#command-summary)
        

--------------------------------------------------------------------------------------------------------------------

<div style="page-break-after: always;"></div>

## Quick start

1. Ensure you have Java `11` or above installed in your Computer.

1. Download the latest `swee.jar` from [here](https://github.com/AY2021S1-CS2103T-T17-2/tp/releases).

1. Copy the file to the folder you want to use as the _home folder_ for SWEe!.

1. Double-click the file to start the app. The GUI similar to the image below should appear in a few seconds. Note how the app contains some sample data. <br>
    ![Quick Start UI](images/QuickStartUi.png)
    <div style="page-break-after: always;"></div>
1. Type the command in the command box and press Enter to execute it.<br>
   Some example commands you can try:

   * **`add q/What does OOP stand for? a/Object Oriented Programming c/General`** : Adds a flashcard with a question and answer into the General category.

   * **`delete 3`**: Deletes the 3rd flashcard in the current list.
   
   * **`list`** : Lists all flashcards.

   * **`review`** : Reviews the current list of flashcards.
   
   * **`view 1`** : Views the 1st flashcard in the current list.

   * **`exit`** : Exits the app.
  
1. Refer to the [Features](#features) below for details of each command.

<div style="page-break-after: always;"></div>

## Application layout

The figures below show the annotated version of the graphic user interface. This will help you better identify the various sections and elements in the application, as well as understand the technical terms stated in this documentation.

![filedirectory](images/ug/label1.png)

![filedirectory](images/ug/label2.png)

<div style="page-break-after: always;"></div>

## Notes about the command format
Feeling a little overwhelmed by the command format we use throughout the user guide? Fear not, as this section will guide you along the various command formats and notations we use throughout the user guide!


Format/Notation | Meaning
-----------|-----------------------
`QUESTION` | Words in uppercase are parameters that you should supply. <br> E.g. in `add q/QUESTION`, `QUESTION` is a parameter which can be used as `add q/What is my name?`
`q/QUESTION` | The letter and slash before the parameter is the prefix. You should use this to separate the current parameter from other parameters.
`success` | Words in lowercase are to be specified exactly, meaning word for word. 
`<success|reviewed>` | Items in angle brackets are either/or options. Each option is delineated by a `|`. <br> E.g. `<success|reviewed>` can be used as success or reviewed but not both
`[c/CATEGORY]` | Items in square brackets are optional. You can choose whether you want to specify them. <br> E.g. `q/QUESTION [c/CATEGORY]` can be used as `q/What is my name? c/Name` or `q/What is my name?`
`[t/TAG]...` | Items with ellipsis after them can be used either multiple or zero times <br> E.g. `t/TAG` can be used 0 times or as `t/friend`, `t/friend t/family`, etc

<div markdown="span" class="alert alert-primary">

:bulb: **Tip:** Parameters can be specified in any order. If the command specifies `q/QUESTION a/ANSWER`, you can specify it as `a/ANSWER q/QUESTION` as well 
</div> 

<div style="page-break-after: always;"></div>

## Common Input Fields

This section will help you understand the different fields you will see in [Features](#features). It gives an overview of what they are, how to specify them and any restrictions.

#### General Notes about Input Fields:
* **Can be empty**  means you can specify the prefix but not pass a value.<br>eg. passing `r/` is valid.
* **Cannot be empty** means you have to specify a value when you specify the prefix.<br>eg. passing `c/` is invalid.
* All input fields should not contain other input prefixes. eg. passing in `What is c/?` as a `QUESTION` to `q/QUESTION` is not supported.

<br>

Input Field | Restrictions and how to specify
-----------|-----------------------
`q/QUESTION`    | This is the question on the flashcard.<br>`QUESTION` has no character limit or restrictions (eg. can have spaces).<br>Cannot be empty.
`a/ANSWER`      | This is the answer on the flashcard.<br>`ANSWER` has no character limit or restrictions (eg. can have spaces).<br>Cannot be empty.
`c/CATEGORY`    | This is the category of the flashcard.<br>`CATEGORY` must be alphanumeric and have a maximum of 50 characters. It can consist of multiple words but there should only be 1 space between words.<br>Cannot be empty.
`r/RATING`      | This is the star rating of the flashcard.<br>`RATING` must be a number between 1 and 5 inclusive.<br>Can be empty.
`d/DIAGRAM`     | This is the diagram of the flashcard (associated with a question in the view pane).<br>`DIAGRAM` must be a valid relative or absolute path to a file. <br>Currently only supports file path **without** spaces. <br>eg. image/umlDiagram.png is supported but image/u mlDiagram.png is not supported <br>Only supports the following image file types: jpg, png, jpeg, bmp <br>Can be empty.
`n/NOTE`        | This is the notes of the flashcard (associated with an answer in the view pane).<br>`NOTE` has no character limit or restrictions.<br>Can be empty.
`t/TAG`         | These are tags of the flashcard. A flashcard can have more than one tag.<br>`TAG` must be alphanumeric and have a maximum of 50 characters.<br>Must **only** be one word.<br>Cannot be empty.
`INDEX`         | `INDEX` refers to the index number shown in the displayed flashcard list.<br>Every visible flashcard on the display list has an `INDEX`.<br>`INDEX` must be a positive integer **greater than 0**. eg. 1, 2, 3, …
`KEYWORD`       | `KEYWORD` can be alphanumeric or punctuations. `KEYWORD` has no character limit but there should be no spaces within the keyword. 

<div style="page-break-after: always;"></div>

## Features

### Add a flashcard : `add`

Now let's get started. The first thing you would do on SWEe is to, of course, add flashcards!

Format: `add q/QUESTION a/ANSWER [c/CATEGORY] [r/RATING] [n/NOTE] [d/DIAGRAM] [t/TAG]...`

* Remember that the `QUESTION` and `ANSWER` fields are compulsory while adding a flashcard! The rest are optional.
(Hint: You can always add in the remaining fields subsequently using our [edit command](#edit-a-flashcard---edit)!)
* After a new flashcard is added, the flashcard list will update to include the new flashcard.
* If you are having troubles understanding the format, feel free to refer to [common input fields](#common-input-fields) on what the different fields are and how to specify them.

<div markdown="span" class="alert alert-primary">

:bulb: **Tip:** If the category is not specified, the flashcard  will be assigned to the <b>General</b> category by default.

</div>

Examples:
* `add q/What does OOP stand for? a/Object Oriented Programming` adds a flashcard with only its compulsory fields, a question and an answer.
* `add q/What does OOP stand for? a/Object Oriented Programming r/3 t/cool` adds a flashcard containing a question, an answer, a rating and a tag.
* `add q/What does OOP stand for? a/Object Oriented Programming d/images/diagram.png` adds a flashcard containing a question, an answer and a diagram
by specifying its file path.

<div style="page-break-after: always;"></div>

**Steps for adding a flashcard with diagram**:

**Step 1**: Locate the relative file path of the image file. In this example, our file path is `image/classDiagramExample1.png` 

Root folder containing SWEe Jar file        |  Image directory
:-------------------------:|:-------------------------:
![filedirectory](images/ug/ug_add_step1.png) |  ![filedirectory](images/ug/ug_add_step1.1.PNG)

<div style="page-break-after: always;"></div>

**Step 2**: Type the command `add q/This is an example of a class diagram a/True d/image/classDiagramExample1.png` and press Enter. Remember to include the file extension in `DIAGRAM`

![filedirectory](images/ug/ug_add_step2.png)

<div style="page-break-after: always;"></div>

**Step 3**: Success! The flashcard is added to the flashcard list.

![filedirectory](images/ug/ug_add_step3.png)

<div markdown="span" class="alert alert-primary">:memo: Note:
To add a flashcard without diagram, skip Step 1 and proceed from Step 2.
</div>

<div style="page-break-after: always;"></div>

### Clear all flashcards : `clear` 

Want to delete all flashcards at one go? Clear command clears all flashcard data from the program.

Format: `clear`

**Steps for clearing all flashcards**:

**Step 1**: Type `clear` into the command box and press Enter

**Step 2**: The result display will display a message telling you that all flashcards have been cleared

**Step 3**: The list view will update to show an empty flashcard list

### Delete a flashcard  : `delete`

Realised that a flashcard is now useless or irrelevant? You can simply remove it from your list using our delete command!

Format: `delete INDEX`

* Deletes the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* `INDEX` must be a positive integer eg. 1, 2, 3, …

Example: `delete 3` deletes the 3rd flashcard in the flashcard list.

**Steps for deleting a flashcard**:

**Step 1**: Locate the flashcard you want to delete. In this example, we want to delete the 3rd flashcard from the list. Type `delete 3` into the command box and press Enter 

![filedirectory](images/ug/ug_delete_step1.png)

**Step 2**: The result display will display a message telling you that the flashcard has been deleted 

**Step 3**: The list view will show the updated flashcard list, with the specified flashcard removed

![filedirectory](images/ug/ug_delete_step2.png)

<div style="page-break-after: always;"></div>

<b>

### Edit a flashcard  : `edit`

Yes, we all make mistakes (and typos). Realised that you have a typo in your flashcard? Fret not, you can edit your flashcard details in SWEe by specifying the fields you want to edit!

Format: `edit INDEX [q/QUESTION] [a/ANSWER] [c/CATEGORY] [n/NOTE] [r/RATING] [d/DIAGRAM] [t/TAG]...`

* Edits the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* A minimum of one field has to be given.
* Specifying empty values to `NOTE`, `RATING`, `TAG` or `DIAGRAM` eg. `r/` will remove the corresponding field in the flashcard.

Examples:

* `edit 3 q/What does OOP stand for? c/Acronyms` edits the 1st flashcard’s question and category to be What does OOP stand for? and Acronyms respectively.
* `edit 3 a/Object Oriented Programming t/` edits the 3rd flashcard’s answer and clears all existing tags
* `edit 3 n/Important question! r/` edits the 3rd flashcard’s note and clears rating

<div style="page-break-after: always;"></div>

**Steps for editing a flashcard**:

**Step 1**: Locate the flashcard you wish to edit. In this example, we want to edit the first flashcard's question and category to What does OOP stand for? and Acronyms respectively. Type `edit 1 q/What does OOP stand for? c/Acronyms` into the command box and press Enter

![filedirectory](images/ug/ug_edit_step1.PNG)
<div style="page-break-after: always;"></div>

**Step 2**: The result display will show a message that the flashcard has been edited successfully

**Step 3**: The list view will show the updated details of the flashcard after the edit

![filedirectory](images/ug/ug_edit_step2.PNG)

<div style="page-break-after: always;"></div>

### Filter for flashcards  : `filter`

Want to look at flashcards belonging to a certain category? Or look at flashcards with a rating of 5?
Filter command allows you to filter for specific flashcard(s) based on your field input(s). 
This will return all the flashcards whose fields match all the fields specified by you.

Format: `filter [c/CATEGORY] [r/RATING] [f/<yes|no>] [t/TAG]...`

* Filters the specified flashcard based on category, rating, favourite status or tags.
* Specifying `f/yes` filters for favourited flashcards while `f/no` filters for unfavourited flashcards.
* Supports filtering of one or more different fields. For example:
    - `filter c/SDLC r/5` will filter out flashcards belonging to the SDLC category with a rating of 5.
* Refer to [common input fields](#common-input-fields) on what the different fields are and how to specify them.
* Although all fields are optional, a minimum of one field has to be given.
<div markdown="span" class="alert alert-primary">:memo: Note:
<code>filter r/</code> will filter for all unrated flashcards.</div>

<div markdown="span" class="alert alert-primary">

:bulb: **Tip:** Want to list all your flashcards after using `filter`? Use the [list](#list-all-flashcards--list) command.

</div> 

Examples:
*  `filter c/SDLC` filters and lists all flashcards belonging to the SDLC category.
*  `filter t/examinable t/study` filters and lists all flashcards that have both an “examinable” tag and a “study” tag.
*  `filter r/3 f/yes` filters and lists all favourited flashcards that have a rating of 3.
*  `filter f/no f/yes c/General` filters and lists all favourited flashcards that belong to the General category.
    (only last instance of f/ is read)

<div style="page-break-after: always;"></div>
**Steps for filtering for a flashcard based on category and tag**:

**Step 1**: We want to filter for a flashcard which has a Trivial category and contains the preloaded tag. Type the command `filter c/Trivial t/preloaded` and press Enter.

![filedirectory](images/ug/ug_filter_step1.PNG)

**Step 2**: The flashcard with the category Trivial and tag field preloaded is shown.

![filedirectory](images/ug/ug_filter_step2.PNG)

<div style="page-break-after: always;"></div>

### Favourite a flashcard  : `fav`

Favourites the specified flashcard.

Format: `fav INDEX`

* Favourites the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* `INDEX` must be a positive integer **greater than 0**. eg. 1, 2, 3, …

Examples: 
* `list` followed by `fav 2` favourites the 2nd flashcard in the displayed flashcard list.

### Unfavourite a flashcard  : `unfav`

Unfavourites the specified flashcard.

Format: `unfav INDEX`

* Unfavourites the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* `INDEX` must be a positive integer **greater than 0**. eg. 1, 2, 3, …

Examples: 
* `list` followed by `unfav 2` unfavourites the 2nd flashcard in the displayed flashcard list.

<div style="page-break-after: always;"></div>

### Find flashcards : `find`

Searches for all flashcards matching any of the search keywords.

Format: `find KEYWORD [KEYWORD]...`
* Finds all flashcards containing any of the keywords.
* Refer to [common input fields](#common-input-fields) on how to specify the different fields.
* The keywords are **case insensitive**.
* Keywords will match as long as they are contained within any flashcard’s question/answer/category/note/tags. eg. `UML` keyword will match a flashcard with a `category` called `UML-Diagram`

<div markdown="span" class="alert alert-primary">

:bulb: **Tip:** Want to list all your flashcards after using `find`? Use the [list](#list-all-flashcards--list) command.

</div> 

Examples: 
* `find general` displays all flashcards containing the word general.
* `find general important` displays all flashcards containing either the word general and/or important.
* `find GENERAL object` displays all flashcards containing either the word general and/or object.
* `find -` displays all flashcards containing "-".

### View help : `help`

Opens a window with a link that directs you to our user guide.

Format: `help`

### List all flashcards : `list`

Shows a list of all flashcards. This is useful for removing any `filter` or `find` you have done on the flashcard list.

Format: `list`

<div style="page-break-after: always;"></div>

### Review flashcards: `review`

Reviews the current list of flashcards. This puts the user in review mode and the user can no 
longer input commands to the textbox.

Format: `review`

Upon entering review mode, the following user input will be recognised:
* `↓ key` shows answer and notes of the current flashcard  
* `↑ key` hides answer and notes of the current flashcard  
* `→ key` moves on to the next flashcard (if there is a next flashcard)
* `← key` moves to the previous flashcard (if there is a previous flashcard)
* `q` quits review mode

<div markdown="span" class="alert alert-primary">:memo: Note:
The review and success frequency of a flashcard is <b>not affected</b> by review mode.
</div>
<br>

<div style="page-break-after: always;"></div>

**Steps for entering review mode**:

**Step 1**: We want to enter review mode to review our flashcards. Type the command `review` and press Enter.

![filedirectory](images/ug/ug_review_step1.PNG)

**Step 2**: We are brought into review mode. The instructions on how to navigate review mode will be shown at the top.

![filedirectory](images/ug/ug_review_step2.PNG)

<div style="page-break-after: always;"></div>

**Step 3**: In this example, we will demonstrate the behaviour of the `↓ key`. Upon pressing the `↓ key`, the answer of the flashcard is shown.

![filedirectory](images/ug/ug_review_step3.PNG)

<div style="page-break-after: always;"></div>

### Quiz flashcards: `quiz`

Quizzes the current list of flashcards. This puts the user in quiz mode and the user can no longer input commands to the textbox.

Format: `quiz`

Upon entering quiz mode, the following user input will be recognised:
* `↓ key` shows answer and notes of the current flashcard  
* `q` quits quiz mode
* `y` This input will only be recognised after the `↓ key` is pressed. `y` is a feedback to indicate a correct answer. 
* `n` This input will only be recognised after the `↓ key` is pressed. `n` is a feedback to indicate an incorrect answer. 

Upon pressing the `↓ key`, the user will be prompted if they got the answer correct. The user can then press 
`y` to feedback that they got the correct answer or `n` to feedback that they got an incorrect answer.  

The quiz mode works in conjunction with the [statistics](#view-the-statistics-of-flashcard--stats) feature. Quiz attempts are recorded and information about the success frequency can be displayed using the [statistics](#view-the-statistics-of-flashcard--stats) feature.
* Pressing `y` will increase the review and success frequency of the flashcard.
* Pressing `n` will increase the review frequency of the flashcard.

<div markdown="span" class="alert alert-primary">:memo: Note: Once the user presses <code>y</code> or <code>n</code>, the review and success frequency of the flashcard is updated accordingly even if the user quits the quiz prematurely.
</div>
<br>

<div style="page-break-after: always;"></div>

**Steps for entering quiz mode**:

**Step 1**: We want to enter quiz mode to test ourselves on the current list of flashcards. Type the command `quiz` and press Enter.

![filedirectory](images/ug/ug_quiz_step1.PNG)

**Step 2**: We are brought into quiz mode. The instructions on how to navigate quiz mode will be shown at the top.

![filedirectory](images/ug/ug_quiz_step2.PNG)

<div style="page-break-after: always;"></div>

**Step 3**: In this example, we will demonstrate the behaviour of the `↓ key`. Upon pressing the `↓ key`, we will be prompted if we got the answer correct.

![filedirectory](images/ug/ug_quiz_step3.PNG)

**Step 4**: We got this answer correct so we will press `y`. This will automatically bring us to the next flashcard.

![filedirectory](images/ug/ug_quiz_step4.PNG)

<div style="page-break-after: always;"></div>

### Sort all flashcards : `sort`

Want to get an overview of how skilled you are at answering the flashcards? Our sort command is here to help you, with two important criteria that you can sort your flashcards by, namely the review frequency and success rate of your flashcards!

Format: `sort <success|reviewed> <-a|-d>`

* Specifying `-a` means sorting by the criteria in ascending order.
* Specifying `-d` means sorting by the criteria in descending order.

Examples: 
* `sort success -a` sorts the flashcards according to success rate in ascending order
* `sort success -d` sorts the flashcards according to success rate in descending order
* `sort reviewed -a` sorts the flashcards according to review frequency in ascending order
* `sort reviewed -d` sorts the flashcards according to review frequency in descending order

**Steps for sorting flashcards**:

**Step 1**: In this example, we want to sort the flashcards according to success rate in an ascending order. Type `sort success -a` into the command box and press Enter

![filedirectory](images/ug/ug_sort_step1.png)
<div style="page-break-after: always;"></div>

**Step 2**: The result display will show a message telling you that the flashcards have been sorted according to success rate in ascending order

**Step 3**: The list view will show the newly sorted list of flashcards according to the criteria

![filedirectory](images/ug/ug_sort_step2.png)

<div style="page-break-after: always;"></div>

### View a flashcard  : `view`

Views the specified flashcard. A "snapshot" of the flashcard is taken and displayed in the view pane to the user.

Format: `view INDEX [-a]`

* Views the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* `INDEX` must be a positive integer **greater than 0**. eg. 1, 2, 3, …
* If `-a` is specified, the answer and notes of the flashcard will be shown too.

Examples:
* `view 1` shows the 1st flashcard (in the displayed flashcard list) on the view pane without answer and notes.
* `view 1 -a` shows the 1st flashcard (in the displayed flashcard list) on the view pane with answer and notes.

<div markdown="span" class="alert alert-primary">:memo: Note: Once another command is executed, the view pane will be returned to a blank state even if the shown
flashcard was not modified/deleted.
</div>
<br>

<div style="page-break-after: always;"></div>

**Steps for viewing a specific flashcard**:

**Step 1**: Locate the flashcard you wish to view. In this example, we want to view the flashcard at index 3. Type the command `view 3` and press Enter.

![filedirectory](images/ug/ug_view_step1.PNG)

**Step 2**: We will be presented with a "snapshot" of the flashcard at index 3 in the view pane.

![filedirectory](images/ug/ug_view_step2.PNG)

<div style="page-break-after: always;"></div>

**Step 3**: To view the answer and notes (if applicable) of the flashcard on the view pane. Type the command `view 3 -a` and press Enter.

![filedirectory](images/ug/ug_view_step3.PNG)

**Step 4**: The answer of the flashcard is displayed on the view pane.

![filedirectory](images/ug/ug_view_step4.PNG)

<div style="page-break-after: always;"></div>

### View the statistics of flashcard : `stats`

View the statistics of a flashcard.

Format: `stats INDEX`

* Shows the statistics of the flashcard at the specified `INDEX`. The `INDEX` refers to the index number shown in the displayed flashcard list.
* `INDEX` must be a positive integer **greater than 0**. eg. 1, 2, 3, …

Example:
* `stats 1` shows the statistics of the 1st flashcard (in the displayed flashcard list) on the view pane.

The statistics feature works in conjunction with the [quiz](#quiz-flashcards-quiz) feature.

The following information will be displayed on the view pane:
* Question of the flashcard (may be truncated for brevity).
* Reviewed count of the flashcard.
* Correct count of the flashcard.
* Pie chart to show the graphical representation of correct attempts vs wrong attempts in quiz mode of the flashcard. (No pie chart will be shown if the flashcard has not been reviewed.)

<div markdown="span" class="alert alert-primary">:memo: Note: Once another command is executed, the view pane containing the statistics will be returned to a blank state even if the shown
flashcard was not modified/deleted.
</div>
<br>

<div style="page-break-after: always;"></div>

**Steps for viewing the statistics of a specific flashcard**:

**Step 1**: Locate the flashcard you wish to view the statistics of. In this example, we want to view the statistics of the flashcard at index 1. Type the command `stats 1` and press Enter.

![filedirectory](images/ug/ug_stats_step1.PNG)

**Step 2**: The statistics of the flashcard at index 1 will be displayed in the view pane.

![filedirectory](images/ug/ug_stats_step2.PNG)

<div style="page-break-after: always;"></div>

### Exit the program : `exit`

Exits the program.

Format: `exit`

### Saving the data

Flashcards data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

--------------------------------------------------------------------------------------------------------------------

<div style="page-break-after: always;"></div>

## FAQ

**Q**: What does it mean if some action is **not supported**?<br>
**A**: It means that our app is not intended to allow said action to work although it may work under certain circumstances.
If you still want to perform the action, do take note that you may face unintended or unexplained behaviour.

**Q**: What is the difference between review mode and quiz mode?<br>
**A**: Review mode is like a sandbox mode where you can move back and forth between flashcards. In quiz mode, you can only go forward. Also, quiz mode asks you for feedback and keeps track of statistics but review mode doesn't.

**Q**: Are success frequency and correct count of a flashcard the same thing?<br>
**A**: Yes. They both refer to how many times you answered with `y` in quiz mode for the flashcard.

**Q**: Why doesn't review mode affect review frequency/count of a flashcard?<br>
**A**: We know the naming may be a little bit confusing but just keep in mind that review mode does **not** affect the statistics (success, review frequency) of a flashcard. Only quiz mode does!

**Q**: What is the success rate of a flashcard?<br>
**A**: Success rate of a flashcard is measured by `(success frequency) / (review frequency) x 100%`. If a flashcard has a review frequency of 0, then its success rate will be 0%.

--------------------------------------------------------------------------------------------------------------------

<div style="page-break-after: always;"></div>

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add q/QUESTION a/ANSWER [c/CATEGORY] [n/NOTE] [r/RATING] [d/DIAGRAM] [t/TAG]...` <br> eg. `add q/What does OOP stand for? a/Object Oriented Programming c/General n/Important question! d/images/diagram.jpeg`
**Clear** | `clear`
**Delete** | `delete INDEX` <br> eg. `delete 3`
**Edit** | `edit INDEX [q/QUESTION] [a/ANSWER] [c/CATEGORY] [n/NOTE] [r/RATING] [d/DIAGRAM] [t/TAG]...` <br> eg. `edit 3 q/What does OOP stand for? a/Object Oriented Programming`
**Filter** | <code>filter [c/CATEGORY] [r/RATING] [f/<yes&#124;no>] [t/TAG]...</code> <br> eg. `filter t/examinable r/3`
**Fav** | `fav INDEX` <br> eg. `fav 1`
**Unfav** | `unfav INDEX` <br> eg. `unfav 1`
**Find** | `find KEYWORD [KEYWORD]...` <br>  eg. `find general important`
**Help** | `help`
**List** | `list`
**Review** | `review`
**Quiz** | `quiz`
**Sort** | <code>sort <success&#124;reviewed> <-a&#124;-d></code> <br> eg. `sort success -a`
**View** | `view INDEX [-a]` <br> eg. `view 1`
**Stats** | `stats INDEX` <br> eg. `stats 3`
**Exit** | `exit`
