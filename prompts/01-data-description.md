# 1. What do I have, and what is wrong with it?

Use this first, on any dataset you have not described yet, before you clean anything and before you ask anything interesting. The AI reads the files and produces a written description of them: what is in each one, what every column means, how the files relate, what is already broken, and a numbered list of the decisions you will have to make before the data can be used. It writes that description to `01_data_description.md` and the code behind it to `01_describe_data.py`, so both are on disk rather than lost in a chat window.

Connect the folder holding your files, then paste the whole thing. The `WHAT I ALREADY KNOW` block is optional: fill it in if you have been told something about the data, leave it empty if you have not. Budget ten minutes to run and twenty to read the output properly.

```text
ROLE
You are a careful data analyst helping me understand a dataset. I am not a
programmer. Your job is to describe what is here and
to point out anything wrong with it. Your job is NOT to fix, clean, or change
anything, and NOT to draw conclusions about what the data means.

DATA
The files in the folder I have connected. Treat them as one dataset.

WHAT I ALREADY KNOW  (optional, leave empty if you know nothing)
[ Anything you have been told or believe about this data. ]

DO THIS
1. For each file: how many rows, how many columns, what one row represents.
2. A table of every column: its name, what you think it means in plain
   English, whether that meaning is confident or a guess, what kind of value
   it holds, how many values are missing, and one real example.
3. How the files relate, which column joins them, and whether every row in
   each file has a match in the others.
4. Five real rows, shown exactly as they appear in the file.
5. Anything wrong, risky, or surprising: missing values, duplicates, columns
   holding more than one thing in a cell, impossible values, columns
   calculated from others that may no longer agree, and anything whose type
   could be misread. Give a count and one real example for each.
6. If I wrote anything under WHAT I ALREADY KNOW: a table with one row per
   claim, giving the claim, what the files actually show, and a verdict of
   confirmed, contradicted, or cannot tell from this data.
7. A list titled "Things I am not sure about": anything you guessed, and
   anything here that could easily be misread.

SHOW YOUR WORKING
- Save the document itself as 01_data_description.md in this folder. Do not
  only print it in the chat.
- Save your code as a separate file, named exactly 01_describe_data.py.
- Do NOT paste the whole script into the document. Instead include a section
  called "How to run this": what needs installing, the exact command, roughly
  how long it takes, and what it prints.
- Explain in plain sentences what the code does and why you did it that way,
  and state how you loaded each column, what type you gave it, and why.
- List any choice that could reasonably have gone differently and would
  change the answer.

DECISIONS FOR ME
End with a numbered section titled "Decisions I need to make before
cleaning". One entry per decision, each with, in this order:
  - What the issue is, in one sentence.
  - The realistic options, as a short list.
  - What each option costs or risks.
  - Which one you would pick if it were yours, and why.
Only include decisions where a reasonable person could choose differently.
Anything with one obviously correct answer belongs in the problems section.

OUTPUT
Markdown. Real tables, not lists pretending to be tables. Plain English, and
define any technical word the first time it appears. In this order: files,
columns, relationships, sample rows, problems, what I told you checked,
things I am not sure about, how to run this, decisions I need to make before
cleaning. Then stop.

DO NOT
- Do not clean, fix, or transform anything.
- Do not tell me what the data means or what I should conclude from it.
- Do not paste the full script into the document.
- Do not present a guess as a fact.
- Do not treat anything I told you as verified. Check it.
```

Keep `01_data_description.md`. The next prompt works from its "Decisions I need to make before cleaning" section, so do not delete it or move it out of the folder.

## Reading the output

Four things are worth checking before you trust any of it, and all four are things the file can settle.

**Ask how it got a number.** Take one count from the problems section and ask "how did you get that number, and show me the rows". Counts that come from reading a column the wrong way look exactly like counts that are right.

**Look at the column table for guesses.** The column named "confident or a guess" exists so that you can see where the description is really an interpretation. Anything marked as a guess is yours to confirm, and it is usually confirmed by asking somebody who made the data rather than by asking the AI again.

**Check anything a spreadsheet might have changed.** Long identifiers, codes with leading zeros, dates in an ambiguous order. These are the errors that produce no warning at all.

**Read the decisions section as the real output.** The description is the part that looks impressive. The list of decisions is the part that determines whether your analysis is any good, and every entry in it is a judgment the AI cannot make for you.

## Notes on changing it

Add to the `WHAT I ALREADY KNOW` block freely, including things you are unsure about, since the whole point of the block is that each claim comes back checked. What you should not do is delete the paragraph underneath it: without the instruction to treat your knowledge as a claim, whatever you write becomes the frame the description is written inside, and the file loses its chance to contradict you.

Keep the instruction not to fix anything. Describing and repairing are separate jobs, and a tool that does both at once will quietly clean something you would have wanted to see.
