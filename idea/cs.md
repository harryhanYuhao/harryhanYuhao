# CS ideas

## Tiny Projects

- Benchmarking L1, L2, L3 cache lantency and intercore latency
- autopull: pull git repo automatically

## Short Term Ambition

### Latin Parser

The only available latin parser online is whitaker's words. Which, I think is obselete.

Create a latin parser that parse the latin words to its stem, declension, congugation, etc. 

Also, it shall be able to scan hexameters.

### Tex Project Manager

It is very cumbersome to manage tex projects: latex generates a lot of dump files; each latex project needs to be starting with a lot of bioler plate code, etc, there is no formatter, linter. LPS is barely working, etc.

So there is a need for tex project manager, like cargo for rust or npm for nodejs.

Format latex files. This formatter shall: 

- Create nice line breaks 

For line breaks within prose, the formatter shall break the line at the same position as the pdf.

### Rust raw mode library

There are severl existing rust raw mode library, but they seems to be incompetent.

## Long Term Ambition

### Math library

Math library for efficient and accurate computation.

### 3D physics engine for research

A physical engine with good graphics, that is factually accurate, implementing efficient mathamtics algorithms, easy to use, and can be played as a game or used to conduct research.

It can be used to simulate the solar system, pendulums, fluid dynamics, etc. 

Importantly, I want it to be like a game. That is, it is easy to use, intuitive, have good interface and graphics, available on most platforms, etc.

### Mathematics Graphics engine

There are still limited graphing software for math, including free software like desmos or proprietary software like Mathematica. Their graphing capabilities, especially for compilcated graphs with implicit functions, non algebraic functions, or multidimension graphs, are greatly limited.

I want to create a capable graphing software that is free, easy to use, and produce beautiful and accurate results.

### Project: Latex Substitute

We love latex, because it is the most, if not the only one, competent tool that empower us to typset professional level documents with our PC. We hate latex, because it contain so much of obscurity that have caused us endless trouble during typsetting. 

So I want to create a latex substitute. 

Computer typsetting seems to be a field that is neglected by most: hackers, programmers, and others with ability to create such a system are occupied by more lofty subjects such as the kernel, AIs, and the web. 
Those most in need of such a new system, who delve hours of their time struggling with tex, are mathematicians, physicists, chemists, even classists, who do not even dream of such an enterprise. '
Indeed the creator of tex was the combination of both: Donald Knuth is one of the best mathematician and programmer of our time. 

#### Other simialr project

- typst: written in rust. Markdown style format, still in early development stage and seems to lose its activity.
- Luatex, Xetex, etc: improvement on tex engine

#### Goal

A tool to help ordinary people to typset professional level documents with ease. So far, I think this tool shall be in the form of a mark down style computer language.

#### To accomplish the project

- Learn what makes a good computer language
- Learn typsetting, formmating, and art.
- Learn make up of pdf.

#### Resource

- Digital Typography, Donald E. Knuth. Book
- Poppler, a C++ pdf library
- xpdf, an open source pdf viewer and toolkit
- ghostscript

