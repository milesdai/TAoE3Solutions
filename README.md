# Solutions for *The Art of Electronics, 3rd ed.*

## Overview
This is an ongoing project to write an open set of solutions to problems in *The Art of Electronics, 3rd ed.* by Paul Horowitz and Winfield Hill. 

## LaTeX Styleguide
To keep the style consistent throughout the document, there is a set of LaTeX macros located in [taoesolutions.sty](./taoesolutions.sty).

### Preamble
All documents should start with
```
\begin{article}
\usepackage{taoesolutions}
```
If for some reason, there is a package needed by only one document, then add a `\usepackage{packageName}` after using taoesolutions. However, it is likely that if the package is needed in one document, it will be necessary in other documents as well, so it might be better just to modify [taoesolutions.sty](./taoesolutions.sty) to import it for all documents.

### Document Formatting
#### Title
Use `\title{titleName}` to create a title at the top of the document with the name `titleName`. Note that this overrides LaTeX's default `\title{}` function.

Important: for consistency, each title should be of the form: *Solutions for Chapter n*, where n is the chapter in question.

#### Exercises
For each exercise, use `\ex{exerciseNum}` to create a header for that particular exercise. Use the full number of the exercise (e.g. 1.10) for `exerciseNum`. You only need the number, not the word "Exercise". 

#### Solutions
Solutions should follow each Exercise header (see above). Write these with plain text in LaTeX. Use any ordinary math environments as necessary.

Within a math environment, several macros have been defined to make formatting easier. They are outlined in the table below.

| Command   | Description   |
|:---:      | ---           |
| `\V`      | Displays V in text form (non-italicized) within a math environment. Equivalent to `\text{V}`. |
| `\A`      | Displays A in text form within a math environment. Equivalent to `\text{A}`. |
| `\Ohm`    | Displays uppercase omega. Equivalent to `\Omega`.
| `\W`      | Displays W in text form. Equivalent to `\text{W}`.
| `\C`, `\H`| Displays each letter in text form within a math environment. Equivalent to `\text{letter}`.|
|`\in`, `\out`, `\Th` | Displays each one in text form within a math environment.|

For solutions with a single, concise answer (i.e. solutions that are just a number of a single phrase of text), use `\mans{ans}` inside a math environment and `\tans{ans}` inside a text environment to indicate the final answer. These commands bold the answer and surround it with a box for emphasis and ease of checking. If a problem is a proof or an explanation, then this kind of emphasis does not really make sense, so do not use these commands. Just write the answer as usual.

#### Drawing Circuits
It may be helpful in your solution to provide circuit drawings. This can be accomplished using the included custom environment
```
\begin{circuit}{label}{caption} 
    ...
\end{circuit}
``` 
This macro handles all the boilerplate code for the circuitikz pacakge. Simply type circuitikz code directly in the body of the environment.

Also note that each circuit should be accompanied by a label and a caption. The caption is a standard Latex caption, and the label is a standard Latex label that can be referenced. To keep all labels descriptive and unique, use the following convention for all labels:
```
fig:<chapterNum>.<exerciseNum>.<figureNum>
```
For example, for the fourth image/circuit in the solutions for exerise number 3.2, we will use 3.2.4 as the label. Use this notation for images as well as circuits (which are just treated internally as images).

#### Miscellaneous
* `\todo{noteToSelf}` is a handy macro that will insert `noteToSelf` in bolded red text withing the final document as a reminder of unfinished work.

## Writing Solutions
When writing solutions, do not repeat the original problem statement so as to not violate copyrights. Assume the reader has read the problem and has access to all the same variables presented in the problem and any iamges the problem may reference.

Make sure you are explaining all your steps as well as any formulas used. Do not just apply a formula without at least briefly mentioning it. (Use your best judgement; there is probably no need to explain V=IR in Chapter 5, but in Chapter 1, that might be a good thing to note when you apply it.)

If possible, explain the thought process behind arriving at the solution instead of just throwing out formulas. This helps people learn how to approach new circuits rather than limiting them to circuits they seen before.