# CRu-ART Stand-in Tracker

A lightweight, single-file web application designed to track operational position logs, monitor sign-on times, and automatically calculate elapsed time on position. It provides instant situational awareness for time-on-position limits and requires no backend, installation, or external dependencies.

## Features

* **Live Zulu Clock & Automatic Time Calculation:** Features a real-time Zulu clock. It automatically calculates the elapsed time (HH:MM) since a user signed onto a position, seamlessly handling midnight crossovers.
* **Smart Summary Table:** A master summary dashboard automatically identifies the current (most recent) person on each position and sorts them by longest time on position at the top.
* **Time-on-Position Alerts:** Elapsed times in the summary table automatically change color to warn of fatigue limits:
* **Yellow (Warning):** 75+ minutes on position.
* **Red (Danger):** 90+ minutes on position.


* **Exclusion Toggles:** Easily exclude specific positions from the Master Summary Table using the checkbox on each position card (useful for combined positions or unused sectors).
* **Data Portability (CSV):** Export your entire log to a CSV spreadsheet for record-keeping or reporting. You can also import a previous CSV to fully restore a session.
* **Persistent Data:** Uses browser `localStorage` to save all entries and exclusions. If you accidentally refresh or close the tab, your data remains intact.
* **Custom Modals & Theming:** Built-in Light/Dark mode (which saves your preference) and custom-themed warning pop-ups to prevent accidental data deletion.

## How to Use

1. **Run the App:** Download the HTML file (e.g., `cru-art.html`) and double-click it to open it in any modern web browser.
2. **Add an Entry:**
* Scroll to the specific position card in the grid.
* Type the controller's initials (automatically capitalizes and jumps to the next box).
* Type the 4-digit Zulu sign-on time (e.g., `1430`) and hit **Enter** or click the **+** button.


3. **Manage the Summary:** Check the "Exclude from Summary" box on a position card if you don't want it heavily monitored on the main dashboard.
4. **Export/Import:** Use the top toolbar to download your log as a CSV file at the end of a shift, or import one to pick up where you left off.
5. **Clear Data:** Click "Clear All Data" at the start of a new day or shift to wipe the board clean (prompts for confirmation).
6. **Print:** Click "Print Document" to print a clean, UI-stripped version of the logs.

## Customizing the Code

Because this is a standalone file, you can easily customize the tracked positions and time thresholds by opening the HTML file in any text editor.

### Modifying the Positions Grid

Find the `positions` array in the JavaScript section and update it with the exact sector or position names for your facility:

```javascript
const positions = ["L", "B", "D", "P", "S", "G", "F", "FDR", "XC", "LC", "GC", "FDT", "SR", "SR2", "SC"];
// Simply add, remove, or rename the strings in this list.

```

### Modifying the Time Alerts

If your facility has different time-on-position limits, locate the `updateSummaryTable()` function and adjust the numeric thresholds (in minutes):

```javascript
if (item.elapsedMinutes >= 90) { // Change 90 to your maximum limit
    timeClass = 'time-danger'; 
} else if (item.elapsedMinutes >= 75) { // Change 75 to your warning limit
    timeClass = 'time-warning'; 
}

```

## Technical Stack

* **HTML5 / CSS3:** Uses CSS Grid for the responsive position cards and CSS variables for seamless dark/light theme switching.
* **Vanilla JavaScript:** Handles all data management, live clock synchronization, elapsed time math, file parsing (CSV), and local storage without relying on external libraries. Includes custom Promise-based modals to replace ugly native browser `alert()` and `confirm()` dialogs.
