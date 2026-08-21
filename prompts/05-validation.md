# 5. Have the whole thing checked

Run this last, on the same folder, once the dashboard exists. What is under review is not the dashboard on its own but the process that produced it: what the data was, what was cleaned and why, what the charts show, and what the page ends up claiming. The output is a written review with a verdict, an issue list, and a record of what it could not check.

Needs the **data plugin**, because it calls `validate-data`. It reads, it recomputes, and it reports. It does not fix anything, and that is deliberate: a reviewer who edits the work is no longer reviewing it.

The prompt is short because most of a good review is already written down inside the skill. What is left is the part the skill does not know: that this was a pipeline, not a single analysis.

Command syntax is namespaced by plugin, so it is `/data:validate-data` in most setups. Check yours if it does not resolve.

```text
/data:validate-data

WHAT TO REVIEW
The whole process that produced the dashboard in this folder, not only the
dashboard. In pipeline order:
- 01_data_description.md
- 02_cleaning_log.md and 02_clean_data.py
- 03_charts.md and 03_make_charts.py
- 04_dashboard_notes.md and 04_dashboard.html

REVIEW IT AS A PIPELINE
- Take the steps in order and say what each one decided.
- For every issue, name the step that introduced it, and say whether the
  dashboard's claims still survive it.
- Recompute the numbers on the dashboard cards, and name the ones you could
  not check.

WRITE IT TO 05_validation.md, ADDING TWO SECTIONS TO YOUR USUAL REPORT
- BY STEP: what each step got right, and what it got wrong.
- WHAT I COULD NOT CHECK: anything you took on trust, and what would settle it.

RULES
- Report, do not fix. Do not edit any file.
- Plain English. Define any technical term the first time you use it.
- If a step never wrote down why a choice was made, say so. A missing reason
  is a finding.
```

## What the prompt does not say, and why

Everything below is already inside the skill, which is why asking for it again would only make the prompt longer:

- A verdict on three levels: ready to share, share with caveats, needs revision.
- Issues with a severity attached to each one.
- Calculation spot-checks, done by recomputing key numbers independently.
- A methodology review: was the right data used, was the population defined correctly, were filters and exclusions right, and who is *not* in this dataset.
- A visualisation review, including whether bar charts start at zero and whether a quick reader could be misled.
- A judgment on whether the conclusions are actually supported.
- A list of caveats that must be passed on to whoever receives the work.
- A long catalogue of standard traps it checks against, including averages of averages, survivorship bias, denominator shifts, Simpson's paradox, outliers dragging averages around, and cherry-picked results.

Open the file and read it once. It is worth knowing what you are getting for free, and it is the clearest example in the whole plugin of a skill being somebody's professional checklist rather than a magic trick.

## Reading the review

**The verdict is the least useful line in the file.** Three words at the top, and everything that matters is underneath them. Read the issues and the last section first, then decide for yourself whether the verdict was earned.

**Check that each issue names a step.** That is what makes this a pipeline review rather than four opinions. An issue introduced during cleaning and still affecting the dashboard is a real finding: a decision you made in two seconds is holding up a page you would have sent to somebody. An issue with no step attached is usually a general remark dressed as a finding.

**Treat "verified" as unverified unless a number is shown.** The spot-check section should contain recomputed figures, not reassurances. If it says a card checks out without saying what it computed, it computed nothing.

**Read "what I could not check" as the honest part of the report.** A review of eight files that claims to have checked everything has checked less than a review that names three things it could not reach.

**Watch for statistical language nobody asked for.** The skill's trap catalogue mentions significance and multiple testing, and its sibling skill knows the whole apparatus, so a review may start talking about p-values. If it does, translate it: how big is the difference, how much do the groups overlap, and how many cases are in each. If you would rather it never came up, add a line to the prompt forbidding significance testing.

**Disagree with one finding on purpose.** Pick something you think it got wrong, say so, and watch what happens. A reviewer that folds the moment you push back was never a second opinion. The whole value of this step is that it holds a position you would rather it did not.

## When the review contradicts your own work

Two collisions are likely, and neither is a fault.

`validate-data` checks charts against a rule about axes: start at zero, no truncated or distorted scales. Your dashboard has a compressed-scale option, because one column spans several orders of magnitude and a plain scale makes every other account look identical. The resolution is a judgment you make and record: a 400-fold range needs a compressed scale to be legible, a compressed scale needs a label saying so, and a reader who misses the label will misread the chart.

Its presentation checklist also says chart titles should state the insight rather than the metric. The chart prompt says the opposite, because a title that states an insight is doing interpretation. Both are defensible, they were written for different jobs, and choosing between them is your call rather than the tool's.

Whichever way you go, the reason belongs in the notes, and "the validator told me to" is not a reason.

## The limit of this step

The reviewer is the same kind of system that did the work. It has the same tendency to sound certain, the same tendency to agree with you, and it can miss something obvious while writing four confident paragraphs about something minor. A second opinion from the same family of tool is not an independent one.

What this step genuinely buys you is coverage: a written checklist gets applied to your work, in order, without getting bored. That is worth having, and it is not the same as assurance.

So three human checks survive it, and they are the ones to keep.

Recompute one number yourself, by hand or in a spreadsheet, and see whether you get the same answer.

Show it to somebody who knows the subject rather than the data. They will question the framing, which no checklist does.

And when you share it, state the caveats out loud, in your own words, rather than leaving them in a file nobody opens.

## Notes on changing it

Keep the pipeline instructions. They are the only part the skill does not already know, and without them you get four separate opinions instead of a chain of custody.

Keep "what I could not check". It is the one section a confident model would never write unprompted.

Keep "report, do not fix". A reviewer that edits your files leaves you with no way to see what it disagreed with.

Keep "plain English, define your terms". The skill is written for business analysts and will otherwise talk about MAU, ARR and churn to a room that does not use those words.

If you find yourself adding much more than this, check the skill file first. Most of what you are about to write is probably already in it.
