# Contributing to this Project

The standard format is under review at the moment and may change, but until further notice, follow the [Styleguide](#latex-styleguide).

## Getting Started

To get started with a contribution, first make sure you have a working LaTeX toolchain set up on your machine.

For more instructions on how to use Github and our rebase workflow, check out [CONTRIBUTING_GITHUB.md](CONTRIBUTING_GITHUB.md)

### Requirements

Compiling the document should require any standard LaTeX distribution as well as the following packages:

* amsmath
* circuitikz
* enumitem
* float
* geometry
* siunitx (v2 for now for compatibility)

The pdf documents should be kept up to date with each commit and are there for people who only want to view without recompiling the documents.

The compilation process uses `latexmk`. See this [quick introduction](https://mg.readthedocs.io/latexmk.html) for installation instructions and a tutorial.

### Building

This process may get wrapped in a Makefile or shell script for ease of use, but in the meanwhile, to compile the PDF, it is recommended that you use `latexmk`. Run the following command to build the pdf and remove any auxiliary files afterwards:

```bash
latexmk -pdf main.tex

# Clean out auxiliary files
latexmk -c
```

## Writing Solutions

This section is about writing solutions qualitatively. For information on formatting, see [Solutions](#solutions) under [Document Formatting](#document-formatting)

When writing solutions, do not repeat the original problem statement so as to not violate copyrights. Assume the reader has read the problem and has access to all the same variables presented in the problem and any images the problem may reference.

Make sure you are explaining all your steps as well as any formulas used. Do not just apply a formula without at least briefly mentioning it. (Use your best judgement; there is probably no need to explain V=IR in Chapter 5, but in Chapter 1, that might be a good thing to note when you apply it.)

If possible, explain the thought process behind arriving at the solution instead of just throwing out formulas. This helps people learn how to approach new circuits rather than limiting them to circuits they have seen before.

## LaTeX Styleguide

To keep the style consistent throughout the document, there is a set of LaTeX macros located in [taoesolutions.sty](./taoesolutions.sty).
These macros also define some common electrical-engineering specific terms.

### Document Structure

The root document is located at `main.tex` which assembles the entire project.
This is the file that should be compiled to generate the final document.
Each chapter is located in its own file called `ChapterN.tex` and is included in `main.tex`.

### Document Formatting

In general, take a look at the existing document structure and use that as guidance.
If there are inconsistencies, feel free to open an issue.

To the extent possible, each new line of LaTeX code should go onto its own line.
This is a weaker form of [semantic linebreaks](https://sembr.org/) (requiring only new sentences to be on new lines).

Also, editor configurations (e.g. tabs vs spaces) have been specified in the `.editorconfig` file.
Please conform to this setup.
Most editors today support plugins that will automatically configure your editor based on the editorconfig settings.
See the [editorconfig docs](https://editorconfig.org/) for more information.

#### Chapter

Use `\chapter{chapterName}` to start a new chapter.
For consistency, each title should be of the form: *Solutions for Chapter n*, where n is the chapter in question.

#### Exercises

For each exercise, use `\ex{exerciseNum}` to create a header for that particular exercise.
Use the full number of the exercise for `exerciseNum`(e.g. `\ex{1.10}).
You only need the number, not the word "Exercise".

Solutions should follow each Exercise header.
Write these with plain text in LaTeX.
Use any ordinary math environments as necessary.

##### Units

Units are typeset using the `siunitx` package.
This latest major release of `siunitx` is version 3, but since it is still quite new, we will stick with version 2 to maintain backwards compatibility for now.

The full capabilities of the package can be found in the [documentation](https://mirror.las.iastate.edu/tex-archive/macros/latex/contrib/siunitx/siunitx.pdf).
Sections 2 and 3 are particularly helpful, as are Tables 1-5.

The short version is that units can be indicated using the `\si{}` command, and quantities with units can be indicated using the `\SI{}{}` command.
These commands can be used in text and math environments.
For example,

```latex
\SI{20}{\milli\ampere\per\cubic\meter}
\si{\volt}
```

Additionally, `siunitx` provides several helpful unit abbreviations defined in Table 5.
Some of the more useful quantities are listed below (excerpted from Table 5).

| Unit | Command |
|---   |:---:|
|nanosecond | `\ns` |
|microcsecond | `\us` |
|millisecond | `\ms` |
|second | `\s` |
|microampere | `\uA` |
|milliampere | `\mA` |
| ampere | `\A` |
|kilohertz| `\kHz` |
|megahertz | `\MHz`|
|kilohm | `\kohm` |
|megohm | `\Mohm` |
|volt | `\V` |
|millivolt | `\mV` |
|watt | `\W` |
|milliwatt | `\mW` |
|farad | `\F` |
|decibel | `\dB` |

Whenever possible, use the `siunitx` package to keep the unit formatting consistent, and use the unit abbreviations to shorten the source code of the equations.

##### Math Macros

Within a math environment, several macros have been defined to make formatting easier.
They are defined in `taoesolutions.sty`.
For example, to indicate an equivalent resistance, you can use `$R_\eq$` rather than `$R_{\text{eq}}$`.
Note that `$R_{eq}$` is incorrect typesetting since the "eq" will be in italics as the variable e and q.

##### Boxing Final Answers

For solutions with a single, concise answer (i.e. solutions that are just a number or a single phrase of text), use `\mans{ans}` inside a math environment and `\tans{ans}` inside a text environment to indicate the final answer.
(These commands stand for **m**ath-**ans**wer and **t**ext-**ans**wer.)
These commands surround the answer with a box for emphasis and ease of checking.
If a problem is a proof or an explanation, then this kind of emphasis does not really make sense, so do not use these commands.
Just write the answer as usual.

##### Questions With Parts

TAoE uses letters to indicate parts, so we will follow that convention here.
The enumerate command has already been formatted to use letters, so just use the following format to create different parts in your solution.

```latex
\begin{enumerate}
    \item
    Solution for part (a)
    
    \item
    Solution for part (b)
    ...
\end{enumerate}
```

#### Drawing Circuits

It may be helpful in your solution to provide circuit drawings.
This can be accomplished using the included custom environment

```latex
\begin{circuit}{label}{caption} 
    ...
\end{circuit}
```

This macro handles all the boilerplate code for the circuitikz pacakge.
Simply type circuitikz code directly in the body of the environment -- no need for semicolons or any `\draw` commands that circuitikz requires.
It also automatically applies the `american` style within circuitikz.

Also note that each circuit should be accompanied by a label and a caption.
The caption is a standard LaTeX caption, and the label is a standard LaTeX label that can be referenced.
To keep all labels descriptive and unique, use the following convention for all labels:

```latex
fig:<chapterNum>.<exerciseNum>.<figureNum>
```

For example, suppose the solutions for exercise 3.2 use six different circuit drawings/images.
To label the fourth image/circuit, use fig:3.2.4 as the label.
Use this notation for images as well as circuits (which are just treated internally as images).

#### Miscellaneous

* `\todo{noteToSelf}` is a handy macro that will insert `noteToSelf` in bolded red text within the final document as a reminder of unfinished work.
* `\todoex{exercise}` will create a red TODO indicating that a particular exercise is unfinished.
