# 4. Build something somebody else can read

Run this after the charts, on the same folder. Up to now every step has forbidden interpretation: describe, decide, look, no conclusions. This one is different. You state an objective and an audience, and the dashboard is allowed to make claims in service of them. That is why it comes last, and why the step after it is validation.

Needs the **data plugin**, because it calls `build-dashboard`. What you get is a single HTML file that opens in a browser with no server and nothing installed, plus a written note recording what the dashboard claims and every judgment behind it. The note matters as much as the dashboard: it is what makes the next step possible.

Command syntax is namespaced by plugin, so it is `/data:build-dashboard` in most setups. Check yours if it does not resolve.

```text
/data:build-dashboard

DATA
The cleaned accounts file in this folder, plus the tweets file.
Keep at most 10 posts per account so the file stays small. Unescape 
&amp; and the literal \n in post text. 

OBJECTIVE  (pick one, or write your own)
[ 1. Brief somebody who has never seen this data on what is in it. 
  2. Show what, if anything, separates automated accounts from human ones
     in this data.
  3. Decide which accounts a human reviewer should look at first. ]

AUDIENCE  (pick one, or write your own)
[ 1. A colleague who knows the subject but has never seen this data.
  2. A manager who will give it two minutes and wants the headline.
  3. Somebody new to the topic, who needs the terms explained on the page. ]

WHAT TO BUILD
One line at the top of the page saying what this dashboard is for and who it
is for. Then choose the panels that serve the objective, and no others. For
every panel, record in the notes which part of the objective it serves.

Whatever the objective, include these three:
- CARDS at the top with the headline numbers. Wherever a mean and a median
  differ noticeably, show both and say which one describes a typical account.
- A TABLE with one row per account, sortable by any column.
- A SEARCH box.

Where the objective involves comparing groups, show the distribution of each
number you compare, not only its average, so the overlap between the groups
is visible on the page.

INTERACTION
- Filters for topic, bot or human, and verified, all of them updating every
  panel at once.
- The search box: I type a name or handle and get that account's profile and
  its posts, readable, one per line.
- Sortable columns, and a visible reset.
- A count of how many accounts are currently in view, so nobody reads a
  filtered number as a total.
- On any chart whose values span orders of magnitude, a toggle between the
  plain scale and a compressed one, labelled in plain words, so I can see
  what the choice does to the picture.

HONESTY
- Every number on the page must be computed from the files, never estimated.
- Where a panel needs a judgment, a cut-off, a scale, a way of counting,
  make it, and write it down in the notes.

SAVE, IN THIS FOLDER
- 04_dashboard.html: one self-contained file that opens in a browser with no
  server and nothing to install.
- 04_dashboard_notes.md: the objective, the audience, one line per panel on
  what it claims and which part of the objective it serves, the numbers
  behind the cards, every judgment you made, and a final section titled
  "What this dashboard does not show".
Then list the folder so I can see both files exist, and stop.

DO NOT
- Do not invent accounts, numbers or posts. If something is not in the files,
  say so.
- Do not put a claim on the page that is not written down in the notes.
- Do not make a claim the panels do not support.
```

## Choosing the objective and the audience

**The objective is not decoration here.** The prompt says to choose the panels that serve it and no others, which means three people with three objectives will produce three genuinely different dashboards. A review queue is mostly a sorted, filterable table with a reason attached to each row. A briefing is mostly cards and plain-language labels. A comparison is mostly distributions with the overlap visible. If your dashboard looks the same whichever objective you picked, the objective was ignored, and that is worth pushing back on.

**Write your own if none of the three fits.** The only requirement is that it names a decision or an audience action. "Explore the data" is not an objective, because nothing in the layout follows from it.

**The audience changes the words, not the numbers.** For the two-minute manager, the headline goes at the top and the detail goes below. For somebody new to the topic, terms get defined on the page. Same data, same computations, different page.

## Reading the output

**Read the notes first, then the dashboard.** Every claim on the page should appear in `04_dashboard_notes.md` with the panel that supports it. If the page says something the notes do not, that is the thing to check, and it is usually a sentence somebody's helpfulness added.

**Go straight to "What this dashboard does not show".** It should mention that this is a curated sample rather than a random draw, that the group sizes are uneven, and that the posts are capped per account. If those are missing, they are the first things to ask about, because each one limits what the dashboard is allowed to claim.

**Filter something, then read a card.** Cards should update with the filters, and the count of accounts in view should tell you how many rows the number came from. A card that does not move when you filter is either a deliberate all-data figure or a bug, and you want to know which.

**Use the scale toggle.** Watch one very large account flatten the follower chart on the plain scale, then watch the compressed scale bring the rest of the distribution back. That is not a display trick, it is the reason a mean of 1.35 million and a median of 3,318 can describe the same column.

**Search one account you already understand.** Read its profile and its posts. Individual rows are the only place a dashboard can be caught being wrong about something you can verify by eye.

## Notes on changing it

Keep the no-significance clause. Not because significance testing is illegitimate, but because a p-value in a dashboard is a claim nobody reading it can check, and the honest alternative, showing overlap and group sizes, is both stronger and legible to everyone in the room.

Keep the distribution line if you are comparing groups. `build-dashboard` works from line, bar, doughnut and stacked charts; histograms and box plots are not in its vocabulary, so without asking you get bar charts of averages, which hide the overlap that decides whether a difference means anything.

Keep the two claim rules together. Nothing on the page that is not in the notes, and nothing claimed that the panels do not support. Either one alone lets the artifact and its justification drift apart.

Keep the notes file even if you never read it again. It is the input to the validation step, and it is also the thing you will want in six months when somebody asks where a number came from.
