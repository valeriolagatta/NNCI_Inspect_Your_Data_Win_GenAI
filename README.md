# Inspect Your Data Using GenAI

Five prompts for looking at a dataset with a general-purpose AI assistant. They were written for a workshop taught for Northwestern Network for Collaborative Intelligence at Northwestern University.

The prompts follow one dataset from first sight to something a colleague could read: describe it, decide what to do about its problems, look at its shape, build something for an audience, then have the whole chain reviewed. The five steps are a plain-language adaptation of the data science workflow in Wickham, Çetinkaya-Rundel and Grolemund, *R for Data Science*, 2nd edition (O'Reilly, 2023).

## Contents

`prompts/01-data-description.md`
The assistant describes what is in the files: every column, what it means, how the files relate, and everything already wrong with them. It is instructed not to fix anything and not to draw conclusions. Ends with a numbered list of the decisions you have to make before the data can be used. There is an optional block where you write what you already believe about the data, and every claim in it comes back checked against the files.

`prompts/02-cleaning-decisions.md`
Works from that list of decisions, one at a time. It presents the options and what each would do to the data, then waits for your answer. Nothing is cleaned until you say so. Produces cleaned copies of the files, the code that made them, and a log of every choice and every change.

`prompts/03-charts.md`
You describe the pictures you want in ordinary language and the assistant makes them. Needs the `data` plugin, which supplies the chart-type choice, the labelling and the styling, so the prompt is mostly about what you want to see and where the files should be saved.

`prompts/04-dashboard.md`
You state an objective and an audience, and get one self-contained HTML page built to serve them, plus a written note recording what each panel claims and what the page does not show. This is the first step that is allowed to argue rather than only describe. Needs the `data` plugin.

`prompts/05-validation.md`
Reviews the whole chain rather than the final artifact alone: what each step decided, which step introduced each problem, whether the claims survive it, and what could not be checked at all. Needs the `data` plugin.

## Usage

Copy the contents of a file, fill in the parts in square brackets, and paste it into your assistant. The prompts are meant to be used in order, since each one reads what the previous one wrote.

Unlike prompts you paste into an ordinary chat, these expect a tool that can read and write files in a folder. Connect the folder holding your data before you start. Prompts 01 and 02 work in any assistant that can see your files. Prompts 03, 04 and 05 call commands from Anthropic's `data` plugin.

## Data

A 200-account sample of Twibot-20, a public benchmark from bot-detection research: social media accounts, some run by people and some automated, each already labelled. Nothing in the prompts depends on it. They were written to work on any tabular dataset, and the examples inside them are the only thing you would need to change.

## Notes

These prompts reduce some common failure modes but do not remove them. Language models generate plausible text rather than retrieving facts, so counts, averages and citations can be invented, and the same confident tone accompanies right and wrong answers. Models also tend to agree with the user, which makes agreement a poor signal: if you push back on a finding and it immediately folds, you have learned something about the finding.

The validation prompt is a first pass, not a certificate. It is the same kind of system that produced the work, so it buys you coverage of a checklist rather than an independent opinion. Three checks survive it and none of them needs a tool: recompute one number somewhere else, re-run the cleaning code from the original files and see whether you get the same output, and take one row you actually understand and follow it through to the claim that rests on it.

Anything pasted into a hosted assistant leaves your machine. Check your organisation's rules on confidential data before using these with real work material.

## License

CC BY 4.0. See LICENSE.

Contact: [valerio.lagatta@northwestern.edu](mailto:valerio.lagatta@northwestern.edu)
