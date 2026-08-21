# 3. What shape is it in?

Run this after prompt 2, on the same folder. You describe the pictures you want in ordinary language, the Data plugin decides how to draw them, and you get one image per chart, the code that made them, and a caption file, all saved next to your data.

This one needs the **data plugin** installed, because it calls `create-viz` rather than explaining from scratch how to make a chart. That is the whole point of the version: the chart-type choice, the axis labels, the colour palette, the number formatting and the design rules already live inside the skill, written down by somebody who does this for a living. What is left for you to write is what you want to see and where the files should land.

Command syntax is namespaced by plugin, so it is `/data:create-viz` in most setups. Check yours if it does not resolve.

```text
/data:create-viz

DATA
The cleaned accounts file in this folder, the one prompt 2 wrote. Load the
account id as text, never as a number.

WHAT I WANT TO SEE
[ WRITE IT HERE, in your own words. One request or several. For example:
    "the distribution of follower counts"
    "how many accounts there are in each topic"
    "whether accounts that follow a lot of people get followed back"
    "a small chart per number column, showing its spread" ]

NAME IT AND SAVE IT
Save everything into this folder, not a temporary directory.
- One image per chart, named 03_chart_01.png, 03_chart_02.png, and so on, in
  the order I asked for them.
- The code as one file named exactly 03_make_charts.py, runnable start to
  finish from the cleaned file alone, producing exactly these images.
- The captions as one file named exactly 03_charts.md: for each chart, its
  file name, one sentence on what it shows, and the one line on why that
  chart type.
Then list the folder so I can see every file exists, and stop.

IF I ASK FOR A CHANGE
Change only the thing I named. Keep every other chart identical, including
its file name, and update 03_make_charts.py and 03_charts.md to match.
```

## Writing the request

**Say what you want to see, not which chart to use.** "Whether accounts that follow a lot of people get followed back" is a better request than "a scatter plot of friends against followers", because the first lets the skill pick, and picking well is the part it is good at. If you already know you want a specific chart type, name it and it will use it.

**Ask for few charts at a time.** Two or three, looked at properly, beat six skimmed. The six-chart cap in the prompt is there to stop a vague request turning into a wall of images nobody reads.

**Expect one question when the request is ambiguous.** "The spread of account ages" could mean age in days or creation date, and it is quicker to answer one question than to redraw a chart.

## Reading the output

**Check the caption against the picture.** The caption file says what each chart shows and why that chart type was used. If the sentence and the image disagree, believe the image and ask about the gap. This is the cheapest check available and it catches the case where the code plotted a different column from the one named.

**Look at what happened to the extreme values.** Any column with a very wide range (follower counts are the classic case) forces a decision: plot it raw and one giant value flattens everything else, or transform the scale and the axis stops meaning what people assume it means. Whatever was chosen, it should be visible on the chart. If you cannot tell which happened, ask.

**Rerun the code.** `03_make_charts.py` should reproduce the same images from the cleaned file alone. A chart you cannot regenerate is a screenshot, and it will not survive the first question from a colleague six months from now.

## Notes on changing it

Keep the naming block. Left to itself the skill saves under a name it chooses, in whatever directory it happens to be working in, which is fine for one person exploring and hopeless for anyone comparing notes or looking for a file later.

Keep the change rule. Without it, asking for one edit tends to regenerate everything, with new file names, and the slide you had already made now points at an image that no longer exists.
