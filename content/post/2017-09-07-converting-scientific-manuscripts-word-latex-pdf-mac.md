---
author: justin
comments: true
date: 2017-09-07 04:58:55+00:00
layout: post
link: http://www.justinbagley.org/3129/converting-scientific-manuscripts-word-latex-pdf-mac
slug: converting-scientific-manuscripts-word-latex-pdf-mac
title: Converting scientific manuscripts from Word to LaTeX PDF on Mac
wordpress_id: 3129
categories:
- blog posts
- command line
- LaTex
- Scientific Journals and Publishing
tags:
- command line
- LaTex
- Pandoc
- PDF
- scientific manuscript
- TexShop
- Word
---

[LaTeX](https://www.latex-project.org) is a very powerful document preparation and typesetting system that provides an accessible means for the programming-minded user to prepare beautiful scientific documents of all kinds, including manuscripts, software documentation, theses and dissertations, etc. Because documents typeset in LaTeX exhibit a high degree of professionalism in their design, while also rendering computer- and math-related characters extremely well, LaTeX has become widely used in many fields of science, and in the academe in general. By using a markup language similar to HTML, and which is non-WYSIWYG (What You See Is What You Get), LaTeX provides the user with tremendous control and flexibility in document design during the writing process. A commonly touted benefit is to, ["...leave document design to document designers, and to let authors get on with writing documents."](https://www.latex-project.org/about/)




I got interested in LaTeX as a way of creating more professional documents for preprint and final manuscript submissions to servers/journals. This post describes some of my recent experiences while teaching myself LaTeX _over the weekend_.




Let me start by saying that my intuition at the outset was that I was *not* ready to switch from writing manuscripts in Word to writing a document from scratch--i.e. generating the content of a document itself--within a LaTeX editor like [TeXShop](http://pages.uoregon.edu/koch/texshop/) or [Texmaker](http://www.xm1math.net/texmaker/). The latter simply does not hold the same degree of appeal to me as doing so in a WYSIWYG processor like Word, and I just wasn't ready to make that big of a jump. So, my idea was to start from a scientific manuscript prepared in Word and convert it into LaTeX, with the goal being to learn to improve the design of my final manuscript in LaTeX, i.e. to learn to present my previously generated content in LaTeX with appropriate formatting before final rendering to PDF. ("But perhaps I'll like it and write only in LaTeX in the future though", I thought.) 




#### Dependencies




Software this post is based on: [Pandoc v1.19.2.1](http://pandoc.org/index.html), [TexShop v3.85](http://pages.uoregon.edu/koch/texshop/index.html), [TextWrangler v4.5.12](https://itunes.apple.com/us/app/textwrangler/id404010395?mt=12)...




#### STEP #1: Word to LaTeX




Since I already had Pandoc installed locally, I started from a .docx file containing the final submission draft of one of my recent papers. I opened [Terminal](https://en.wikipedia.org/wiki/Terminal_(macOS)) (my preferred command line interface on Mac) and there I used Pandoc to convert this file from .docx to LaTeX (.tex) format using a basic/default command, with no special options, as follows:




[code language="bash"]
pandoc -s manuscript.docx -o manuscript.tex
[/code]




After doing this, I opened the resulting .tex document in TextWrangler and resaved it with UTF-8 encoding for UNIX; here, I changed the filename from "manuscript.tex" to "manuscript1.tex" and kept both versions in the working directory.




#### STEP #2 – _n_: Editing and Typesetting in TexShop




Next, I opened the .tex doc in TexShop. I tried to typeset to PDF in TexShop, but of course things failed "out of the box" several times. The keyboard shortcut for typesetting your tex doc in TexShop is Command-T; I pressed this several times during my initial attempts. Typesetting failed once due to an erroneous/problematic "Â" character that somehow got added by Pandoc and screwed things up at one point in the manuscript, and a second time due to a UTF-8 command passed to a package called 'inputenc'. I fixed the latter error by simply commenting out the problematic line from the .tex file. The line I commented out was within the first 10 lines of the document and looked like this:




[code language="LaTeX"]
  \usepackage[utf8]{inputenc}
[/code]




After these changes, I was able to get a first, awkward PDF file rendered, and I immediately realized that there were a number of issues that cropped up when going with the defaults: (1) wrong font size, (2) numerous wrongly displayed symbol characters, (3) line numbers disappeared, (4) missing page breaks, (5) improperly formatted tables and table/fig captions, and on and on... It became clear that many additional edits would need to be made to the file in a thoughtful manner to make it even _approximate_ something close to my desired end result.




To make a long story short (_I couldn't go through all the changes that I made, or everything that I learned about LaTeX during this exercise in a single post_), I experimented with adding several packages to the preamble of my .tex file, I read documentation on codes for basic document formatting and code for correctly calling mathematical characters and symbols, I proofread the text and fixed errors, I remade the tables, I fixed page size and rotation, and I gave my bibliography section an appropriate hanging indent format.




##### Preamble-Title Page Template




Through _many additional edits to the document_, **I came up with the following preamble-title page template, which I will probably continue to modify, but you can feel free to start from when making a .tex file for any double-spaced, 12 pt font manuscript:**




[code language="LaTeX"]
\documentclass[12pt]{article}
\usepackage{graphicx}
\usepackage{lmodern}
\usepackage{amssymb,amsmath}
\usepackage{ifxetex,ifluatex}
\usepackage[letterpaper, portrait, margin=1in]{geometry}
\usepackage{setspace}
\doublespacing
\usepackage{lineno}
%%%\usepackage[utf8]{inputenc}
\def\linenumberfont{\normalfont\small\sffamily}
\linenumbers\usepackage{fixltx2e} % provides \textsubscript
\ifnum 0\ifxetex 1\fi\ifluatex 1\fi=0 % if pdftex
  \usepackage[T1]{fontenc}
\else % if luatex or xelatex
  \ifxetex
    \usepackage{mathspec}
  \else
    \usepackage{fontspec}
  \fi
  \defaultfontfeatures{Ligatures=TeX,Scale=MatchLowercase}
\fi
% use upquote if available, for straight quotes in verbatim environments
\IfFileExists{upquote.sty}{\usepackage{upquote}}{}
% use microtype if available
\IfFileExists{microtype.sty}{%
\usepackage[]{microtype}
\UseMicrotypeSet[protrusion]{basicmath} % disable protrusion for tt fonts
}{}
\PassOptionsToPackage{hyphens}{url} % url is loaded by hyperref
\usepackage[unicode=true]{hyperref}
\hypersetup{
            pdfborder={0 0 0},
            breaklinks=true}
\urlstyle{same}  % don't use monospace font for urls
\usepackage{longtable,booktabs}
% Fix footnotes in tables (requires footnote package)
\IfFileExists{footnote.sty}{\usepackage{footnote}\makesavenoteenv{long table}}{}
\IfFileExists{parskip.sty}{%
\usepackage{parskip}
}{% else
\setlength{\parindent}{6pt}
\setlength{\parskip}{10pt plus 2pt minus 1pt}
}
\setlength{\emergencystretch}{3em}  % prevent overfull lines
\providecommand{\tightlist}{%
  \setlength{\itemsep}{0pt}\setlength{\parskip}{0pt}}
\setcounter{secnumdepth}{0}
% Redefines (sub)paragraphs to behave more like sections
\ifx\paragraph\undefined\else
\let\oldparagraph\paragraph
\renewcommand{\paragraph}[1]{\oldparagraph{#1}\mbox{}}
\fi
\ifx\subparagraph\undefined\else
\let\oldsubparagraph\subparagraph
\renewcommand{\subparagraph}[1]{\oldsubparagraph{#1}\mbox{}}
\fi

% set default figure placement to htbp
\makeatletter
\def\fps@figure{htbp}
\makeatother

\usepackage[document]{ragged2e}
\usepackage{indentfirst}
%%%\usepackage{lscape}
\usepackage{pdflscape}

\date{}

\begin{document}

\begin{center}
Original article formatted for \emph{JOURNAL\_NAME}

\vspace{5mm} %5mm vertical space

\large\textbf{MANUSCRIPT\_TITLE}
\normalsize

\textsc{FIRST\_AUTHOR\_NAME\textsuperscript{1,2,*}} and \textsc{SECOND\_AUTHOR\_NAME\textsuperscript{1} }

\textsuperscript{1}\emph{FIRST\_INSTITUTIONAL\_ADDRESS}

\textsuperscript{2}\emph{SECOND\_INSTITUTIONAL\_ADDRESS}

\textsuperscript{*}\emph{Corresponding author.} E-mail:
\href{mailto:FIRST\_AUTHOR\_EMAIL}{\nolinkurl{FIRST\_AUTHOR\_EMAIL}}.

\emph{Running Head:} RUNNING\_HEAD (NUM\_CHAR\_RUNNING\_HEAD
characters w/spaces)

\emph{Word Count:} PAPER\_WORD\_COUNT words, Abstract, main body, plus table and
figure captions; Abstract only,
\protect\hypertarget{OLE_LINK3}{}{\protect\hypertarget{OLE_LINK4}{}{}}ABSTRACT\_WORD\_COUNT
words.
\end{center}

\vspace{5mm} %5mm vertical space
\vspace{5mm} %5mm vertical space

\end{document}

[/code]




**This code contains the preamble and title page for the manuscript ("\end{document}" is added only to round out document structure, so that this code can be copied and pasted into TexShop and rendered). Aside from double spacing and appropriate font size, this setup also causes pages to be numbered and the manuscript to have continuous line numbering throughout, consistent with the required or preferred format of many journals. To use this, all you need to do is copy and paste it in place of the top/preamble section of your manuscript .tex document, then change the uppercase "pothole_case" labels (e.g. "FIRST\_AUTHOR_EMAIL") to the relevant content for your paper.** Here, backslashes are only present in the labels to escape the underscore characters. You can see the "inputenc" line that I commented out at line 10. Right after this, you could add a page break ("\break") and then enter your Abstract, and so on.




**Here is a screenshot of the rendered Preamble-Title Page Template:**




![](http://www.justinbagley.org/wp-content/uploads/2017/09/Preamble-Title_Page_Template_screenshot.png)




##### Example Table Format Using "longtable"




I discovered that, when you convert a Word document to LaTeX using Pandoc, the default table format it spits out is that using the "longtable" environment. There are other ways of making tables in LaTeX, e.g. using "tabular" or "tabularx" environments, that seem to be better suited for some things, and perhaps more popular. However, longtable is probably used as the default because, when tables span multiple pages (be vertically long), it prints the column headings on each page, which can be nice. You can find other examples [online](http://users.sdsc.edu/~ssmallen/latex/longtable.html), but here is an example showing a partial table from my paper, using longtable:




[code language="LaTeX"]
\singlespacing
\footnotesize%%%%%%%%%%%  smaller font size %%%%%%%%
\begin{longtable}[]{@{}llll@{}}
\toprule
\textbf{Subset} & \textbf{No. subset partitions} & \textbf{Total length
(bp)} & \textbf{Best-fit model}\tabularnewline
\hline
\textbf{`\emph{balfouriana}' group}\tabularnewline
1 & 16 & 7579 & HKY+$\Gamma$\tabularnewline
2 & 26 & 11791 & HKY+$\Gamma$\tabularnewline
3 & 4 & 1724 & GTR+$\Gamma$+\emph{I}\tabularnewline
4 & 21 & 9077 & TrN+$\Gamma$\tabularnewline
5 & 9 & 3263 & K80+$\Gamma$\tabularnewline
6 & 7 & 3395 & HKY+$\Gamma$\tabularnewline
7 & 23 & 10129 & HKY+$\Gamma$\tabularnewline
8 & 13 & 6810 & HKY+$\Gamma$\tabularnewline
9 & 2 & 499 & SYM+$\Gamma$+\emph{I}\tabularnewline
10 & 6 & 2237 & SYM+$\Gamma$\tabularnewline
11 & 8 & 3015 & HKY+$\Gamma$+\emph{I}\tabularnewline
12 & 2 & 914 & TrN+$\Gamma$\tabularnewline
13 & 10 & 3688 & K80+$\Gamma$+\emph{I}\tabularnewline
14 & 13 & 4872 & K80+$\Gamma$\tabularnewline
15 & 5 & 1995 & HKY+$\Gamma$\tabularnewline
16 & 1 & 443 & K80+$\Gamma$+\emph{I}\tabularnewline
Total: & 166 & 71,431 & --\tabularnewline
\bottomrule
\end{longtable}
\normalsize
\doublespacing
bp, nucleotide base pairs.
%%%\end{landscape}
[/code]




**Here is a screenshot of the rendered table:**




![](http://www.justinbagley.org/wp-content/uploads/2017/09/Example_Table_Format_screenshot.png)




_That's all for now! More later when I have time!_







~J
