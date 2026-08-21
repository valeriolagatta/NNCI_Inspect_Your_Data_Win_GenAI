# 2. What do I do about it?

Run this after prompt 1, on the same folder. It reads the decisions that prompt 1 wrote down and turns them into an interview: one issue at a time, options, what each would do to the data, a recommendation, and then it waits for you. Nothing is cleaned until you say so. At the end it produces cleaned copies of your files, the code that made them, and a log of every choice you made and every change that followed.

You are the judgment, it is the hands. Budget twenty to forty minutes depending on how many decisions prompt 1 found, and do not run it when you are in a hurry, because the value here is entirely in the answers you give.

```text
ROLE
You are helping me clean this dataset. I am not a programmer. You are the
hands, I am the judgment. Your job is to walk me through the decisions one
at a time and do what I decide. Your job is NOT to decide for me, and NOT to
clean anything before I have said what I want.

INPUT
The file 01_data_description.md in this folder. Work from its section titled
"Decisions I need to make before cleaning".

HOW TO PROCEED
1. First, list the decisions by number with a one-line summary of each, so I
   can see how many there are. Then stop and wait.
2. Then take them ONE AT A TIME. For each, give me:
   - the issue in one or two plain sentences
   - the options, labelled A, B, C
   - what each option would do to the data, in numbers where you can
   - your recommendation and why, in one sentence
   Then ask me which I want, and WAIT for my answer. Do not move on to the
   next decision, and do not assume my answer.
3. If my answer is unclear, or I ask you a question instead of answering,
   answer it and then ask me again. Never guess what I meant.
4. If I say "your recommendation", use it, but say which one that was.

WHEN ALL DECISIONS ARE MADE, PRODUCE ALL FOUR
1. THE CLEANED DATA. One new file per original, named by adding _clean
   before the extension. Never overwrite the originals.
2. THE CODE, as a single file named exactly 02_clean_data.py, runnable from
   start to finish by someone who has only the originals.
3. THE CHANGE LOG, as a file named exactly 02_cleaning_log.md, containing:
   - the date at the top
   - row and column counts of every file, before and after
   - a table with one row per decision: number, issue, options offered,
     what I chose, what you did, how many rows or cells changed
   - a section "Not changed, and why"
   - a section "How to run this" for 02_clean_data.py
4. CONFIRMATION. List the folder and show me every file above exists, with
   its size. If any is missing, say so and write it before you stop.

OUTPUT
During the interview: one decision at a time, nothing else.
At the end: the four items above, in order, ending with the folder listing.
Then stop.

DO NOT
- Do not batch the decisions or present them all at once for one answer.
- Do not finish without writing 02_cleaning_log.md. A cleaning run with no
  written log is not finished, however good the data looks.
- Do not describe the change log in the chat instead of writing the file.
- Do not clean anything I have not approved.
- Do not overwrite the original files.
- Do not silently drop rows or columns. Every change appears in the log.
```

## Sitting through the interview

**Answer in your own words.** You do not have to pick A, B or C. You can propose your own solution based on your understanding of the data. 

**Ask what a number means before you choose.** "Option B drops 412 rows" is not enough to decide on. Ask which rows, and ask to see five of them. Deletions are the changes you cannot inspect afterwards, so they are the ones to slow down on.

**Say "I do not know" when you do not know.** The useful follow-up is "what would I need to find out, and who would know it". That answer usually names a person rather than a method, and going to ask them is the correct move, not a failure of the tool.

**Disagree with one recommendation.** Pick a decision where you think the recommendation is wrong, say so, and watch what happens. Some models will hold their ground and explain why. Some will fold immediately and adopt your view. 

## Reading the log

`02_cleaning_log.md` is the real output of this step, more than the cleaned files are. Three things to check in it.

**The before and after counts.** If a row count changed and no decision explains it, something happened that nobody chose. That is the single most useful line in the file.

**The "Not changed, and why" section.** Problems you decided to live with are as much a part of the record as the ones you fixed, and in six months this section is what stops you rediscovering them from scratch.

**Whether the log matches the data.** Run `02_clean_data.py` on the originals and check you get the same cleaned files. A log that describes a cleaning nobody can reproduce is a story, not a record.

## Notes on changing it

Keep the one-at-a-time constraint. A model asked for all the decisions at once will present them as a batch and take your single reply as approval for the lot, which is exactly the thing this prompt exists to prevent.

Keep the log mandatory and keep it a file. Cleaning that lives only in a chat window is cleaning you cannot defend, and "the AI cleaned it" is not a methods section.

If prompt 1 found more decisions than you have patience for, do not batch them. Tell it to take the first five now and stop, then run the rest later. Ten considered answers beat twenty rushed ones, and the log will show exactly where you stopped.
