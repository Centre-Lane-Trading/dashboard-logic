### Prerequisites
* Clone the repo
* Create a virtual environment (whatever your preferred method is ok)
* Install polars v0.20.16 (`pip install -r requirements.txt`)

Each section is marked by the name of the event that should trigger the function calls.
The parts that need to be implemented in the UI are marked as **TODO**. The values are hardcoded just so you can follow the steps and see expected outputs.

The following example uses the python interactive shell, just to illustrate.

### Important Note
The graph should always match the `board.exclusions_df` DataFrame. This DataFrame automatically keeps track of the user exclusions (by removing those dates).

We need a visual marker to know all the date regions that are excluded. Ideally a gray region in the graph, but we can discuss to determine what makes 
the most sense.

You can easily find out which dates are missing by comparing the "date" values in the `board.original_df` to the ones in the `board.exclusions_df`.

#### Step 0
```
# Start a python interactive shell
# (assuming you have the prerequisites installed, and you are in the code folder)
python

>>> from Leaderboard import Leaderboard
>>> from datetime import date # we will need this to hardcode the example values
```

### On Page Load

* Initialize the leaderboard object
* Summarize the leaderboard
* **TODO:** display the graph of cumulative profit
* **TODO:** display the summary
```
board = Leaderboard()
board.load_csv("/home/abrahame/Downloads/miso_virts_og_study.csv")
board.summarize() # this needs to be displayed, along with the graph
```

### On zoom-in (The user selects an area in the graph)
* **TODO:** Capture the start-date and the end-date of the zoom-in area
* **TODO:** Zoom-in to the selected region in the graph
* Call the zoom_in() function
* Summarize the leaderboad
* **TODO:** display the summary
```
# hardcoded for the example; these should be captured from user input
start_date = date(2024, 10, 1)
end_date = date(2024, 10, 10)

board.zoom_in(start_date, end_date)
board.summarize() # note: summary will look the same at this point (expected behaviour)
```

### On toggle (User clicks the "area-only" toggle; to activate it)
* Call the toggle() function
* Summarize the leaderboard
* **TODO:** display the summary
```
board.toggle()
board.summarize() # note: now the summary will change (expected behaviour)
```

### On pan (User moves forward/backward in the graph)
* **TODO:** Capture the start_date and the end-date
* **TODO:** Refresh the graph (normal panning functionality from any graph)
* Call pan() function
* Summarize the leaderboard
* **TODO:** display the summary
```
# hardcoded start and end date; these should come from user input
# we are simulating user panning two days forward in this example
start_date = date(2024, 10, 3)
end_date = date(2024, 10, 12)
board.pan(start_date, end_date)
board.summarize() # note summary will change again (due to area change)
```

### On toggle (User clicks the "area-only" again; to deactivate it)
Note: same behaviour as the previous toggle click; just to illustrate summary change
* Call the toggle() function
* Summarize the leaderboard
* **TODO:** display the summary
```
board.toggle()
board.summarize() # note: summary changes back to its original values
```

### On exclusion (User selects range of dates to exclude)
* **TODO:** Capture the exclusion start_date and end-date
* **TODO:** Refresh the graph (gray-out excluded area if necessary; see current app)
* Call exclude_region() function
* Summarize the leaderboard
* **TODO:** display the summary
```
# arbitrarily choosen values for this example
start_date = date(2024, 10, 5)
end_date = date(2024, 10, 10)

board.exclude_region(start_date, end_date)
board.summarize()
```

### On toggle (User clicks the "area-only"; to activate it again)
Note: same behaviour as the previous toggle click; just to illustrate summary change
* Call the toggle() function
* Summarize the leaderboard
* **TODO:** display the summary
```
board.toggle()
board.summarize() # note: summary changes (excluded data is not added anymore)
```

### On "group" toggle (User clicks the "group" toggle; to deactivate it)
* Call the group() function
* Summarize the leaderboard
* **TODO:** display the summary
* **TODO:** update graph (it should display 12 lines, instead of 3; one for each policy, node combination)
```
board.group()
board.summarize() # notes: "node" column will appear now; summary will have 12 rows
```

### On Top N input (User inputs integer at "Top N" field, then clicks "confirm" button next to field)
* **TODO:** Capture the value in the field (must be an integer)
* Call the set_topn() function
* Summarize the leaderboard
* **TODO:** display the summary
* **TODO:** update the graph (note: graph doesn't change because grouping is deactivated)
```
# harcode value for the example; this should be coming from user input
topn_val = 2
board.set_topn(topn_val)
board.summarize() # note: no change because of the group toggle (expected behaviour)
```

### On "group" toggle (User clicks the "group" toggle again; to re-activate it)
* Call the group() function
* Summarize the leaderboard
* **TODO:** display the summary
* **TODO:** update graph (it should display 12 lines, instead of 3; one for each policy, node combination)
```
board.group()
board.summarize() # notes: now the summary will change
```

### On "group" toggle (User clicks the "group" toggle again; to deactivate it)
Note: same behaviour as before; this is just to make the "metric" feature easier to see (next step)
* Call the group() function
* Summarize the leaderboard
* **TODO:** display the summary
* **TODO:** update graph (it should display 12 lines, instead of 3; one for each policy, node combination)
```
board.group()
board.summarize() # notes: summary will change back to 12 rows and show the "node" column
```

### On "metric" click (User clicks any of the "PnL", "per MWh", or "win %")
* Call the metric() function
* Summarize the leaderboard
* **TODO:** display the summary
```
# arbitrary value hardcoded for the example; this should come from the user selection
# the only valid values are "PnL", "per MWh" or "win %"
metric_selected = "win %"
board.set_metric()
board.summarize() # notes: the rows in summary will be sorted by "win %"

# simulate user click on "per MWh" column name
metric_selected = "per MWh"
board.set_metric()
board.summarize() # notes: might look the same as "PnL" sorting, by coincidence
```
