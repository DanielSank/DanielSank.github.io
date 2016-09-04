---
title: How to make LaTeX awesomer
header:
  image: header.png
---

LaTeX is an excellent typsetting language.
I use it for all my of my technical documentation both at work and at home.
However, LaTeX is just that, a typesetting language, and is not really suited to doing logic.
This is as it should be; there's no sense in a typesetting language trying to also be a programming language.
There are, however, a few critical little tasks that fall in a gray area between typesetting and programming that LaTeX does not provide, and whos absence makes LaTeX a lot more painful than it would otherwise be.
Some folks address these shortcomings by using a real programming language to generate LaTeX.<sup>1</sup>
I recommend looking into that approach, but here we're going to see how to fill in what I consider to be LaTeX's most important missing features using LaTeX itself.
As we go along, we'll see code listings illustrating each point.
At the beginning of each listing you will find a download link for a zip archive containing a complete working example.

This is a pretty long post.
To skip the pedagogical development and get to the "final answer", see [the modularity demo in my TeXtricks github repo](https://github.com/DanielSank/TeXtricks/tree/master/modularity-demo).

Consider a short article about octopuses ([example A][1])

`(A) octopuses_article.tex`

```latex
\documentclass{article}
\title{Octopuses}

\begin{document}
\maketitle
This is an article about octopuses.

\section{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\section{Camouflage}
Octopuses can change color.
They even change the texture of their skin.

\end{document}
```

So far everything looks good, but now suppose we'd like to include the sections we've written in a book about animals.
We can't, because the preamble items, including the title, documentclass, and `\begin{document}` command, are mixed in with the content we'd like to use in the book.

## Separation of content and preamble

We need some way to separate the *content* of our octopus article from the preamble so that the content can be grabbed wherever we need it.
Let's organize our files into a meaningful directory structure

```
animals_book.tex
octopuses/
-octopuses_content,tex
-octopuses_article.tex
```

and use the `\input` macro ([example B][2])

`(B) octopuses_article.tex`

```latex
% This is a short article about octopuses.

\documentclass{article}
\title{Octopuses}

\begin{document}
\maketitle
This is an article about octopuses.
\input{octopuses_content}

\end{document}
```

`(B) octopuses_content.tex`

```latex
\section{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\section{Camouflage}
Octopuses can change color.
They even change the texture of their skin.
```

Now that the content is separated from the boilerplate, we can re-use the content in our book about animals:

`(B) animals_book.tex`

```latex
% This is a book about several types of animals.

\documentclass{book}
\title{Animals}

\begin{document}
\maketitle
This is an article about animals.

\chapter{Octopuses}
In this chapter, we'll learn about octopuses.
\input{octopuses/octopuses_content}

\chapter{Horses}
This chapter is about horses.

\end{document}
```

Example B is pretty good.
We've established a simple effective pattern of separating our content files from our preamble (the horse chapter's content is in `animals_main.tex`, but that's just to keep the illustration brief).

## Relative paths: [`import`](https://www.ctan.org/pkg/import?lang=en)

The `\input` command is really useful, but it falls short of a total solution for separating content and preamble.
The problem is that the `\input` macro requires the paths to the target file to be specified relative to the directory from which we run the LaTeX compiler.

Suppose our octopus content file grabs a quotation from another file ([example C][3]):

```
animals_book.tex
octopuses/
-octopuses_content,tex
-octopuses_article.tex
-octopus_quote.tex  <-- new file
```

`(C) octopus_content.tex`

```latex
\input{octopus_quote}

\section{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\section{Camouflage}
Octopuses can change color.
They even change the texture of their skin.
```

`(C) octopus_quote.tex`

```latex
\begin{center}
\textit{``We split from our common ancestor with the octopus half a billion years ago.
And yet, you can make friends with an octopus.''} -Sy Montgomery
\end{center}
```

When we run the LaTeX compiler on `octopuses_article.tex` from within the `octopuses/` directory, the `\input{octopuses_content}` command works just fine because `octopuses_content` is the full path, starting in the working directory, to the target file.
The `\input{octopus_quote}` command in `octopuses_content.tex` works for the same reason.
However, when we run LaTeX from the root directory on `animals_book.tex`, the compiler fails with the message `File 'octopus_quote.tex' not found`.
This happens because `\input` needs the full filename starting from the working directory, which in this case is `octopuses/octopus_quote`.
We could fix the compilation error by changing the offending line to `\input{octopuses/octopus_quote}`, but then we wouldn't be able to compile `octopuses_article.tex` from its own directory.
This is a disaster because now a *content* file has to be adjusted depending on which parent document is using that content.<sup>2</sup>

Fortunately, someone else already noticed this problem and fixed it by writing the [`import`](https://www.ctan.org/pkg/import?lang=en) package.
The `import` package provides a drop-in replacement for `\input` but which properly handles relative directories the way we want.
Here's how `import` solves our problem ([example D][4])

`(D) octopuses_article.tex`

```latex
\documentclass{article}
\usepackage{import}
\title{Octopuses}

\begin{document}
\maketitle
This is an article about octopuses.
\subimport*{./}{octopuses_content}
\end{document}
```

`(D) octopuses_content.tex`

```latex
\subimport*{./}{octopus_quote}

\section{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\section{Camouflage}
Octopuses can change color.
They even change the texture of their skin.
```

`(D) animals_book.tex`

```latex
\documentclass{book}
\usepackage{import}
\title{Animals}

\begin{document}
\maketitle
This is a book about animals.

\chapter{Octopuses}
In this chapter, we'll learn about octopuses.
\subimport*{octopuses/}{octopuses_content}

\chapter{Horses}
This chapter is about horses.

\end{document}
```

Thats it, just replace `\input{dir/file}` with `\subimport*{dir}{file}` and all your LaTeX code will handle relative paths properly.

## Relative section headings: [`coseoul`](https://www.ctan.org/pkg/coseoul?lang=en)

We're not done though.
Example D works because `octopuses_content.tex` uses the `\section` heading, which just happens to be the right heading to use underneath the `\chapter` headings used in `animals_book.tex`.
Consider what happens if, instead of a book about animals, we want an article about animals ([example E][5]):

`(E) animals_article.tex`

```latex
\documentclass{article}
\title{Animals}

\begin{document}
\maketitle
This is an article about animals.

\section{Octopuses}
In this section, we'll learn about octopuses.
\subimport*{octopuses/}{octopuses_content}  % Doesn't do what we want

\section{Horses}
This section is about horses.

\end{document}
```

Example E is no bueno.
The `circulation` and `camouflage` parts of the document should be *sub*sections of the Octopus section, but they are in `\section` headings.
The problem, of course, is that `\section` (and other headings) are absolute instead of relative.
Once we've written `octopuses_content.tex` with `\section` we can't use it anywhere else unless `\section` happens to be the right depth.

It turns out someone else aready confronted this problem and developed the [`coseoul`](https://www.ctan.org/pkg/coseoul?lang=en)  package<sup>3</sup> to deal with it.
`coseoul` offers a set of commands that take the place of `\chapter` and `\section`, and instead provide headings whose levels are determined relative to the level in which the commands are invoked:

* `\levelstay{<name>}`: Start a new heading at the *same* level as we are presently in.

* `\leveldown{<name>}`: Start a new heading *one level deeper* than the level we are presently in.

* `\levelup{<name>}`: Start a new heading *one level above* the level we are presently in.

Under the hood, `coseoul` creates a global counter called `currentlevel`.
The three commands work by incrementing or decrementing `currentlevel` and then choosing which heading (i.e. chapter, section, subsection...) to use based `currentlevel`'s value.

To start, here's a *failed* attempt at using `coseoul` ([example F][6]):

`(F) animals_article.tex`

```latex
\documentclass{article}
\usepackage{import}
\usepackage{coseoul}
\title{Animals}

\begin{document}
\maketitle
This is an article about animals.

\levelstay{Octopuses}
\subimport*{octopuses/}{octopuses_content}

\levelstay{Horses}
This chapter is about horses.

\end{document}
```

`(F) octopuses_content.tex`

```latex
\subimport*{./}{octopus_quote}

\levelstay{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\levelstay{Camouflage}
Octopuses can change color.
They even change the texture of their skin.
```

Example F fails in the same way as example E: the Circulation and Camouflage headings are at the same level as the Octopus heading, whereas they should be one level deeper.
We can't fix this by replacing `\levelstay` with `\leveldown` inside `octopus_content.tex`, because then `octopus/octopus_article.tex`'s first heading would be a subsection (try it!).

Example F tells us that the decision of whether to `\levelstay` or `\leveldown` when including a content file needs to be made outside of that content file, because whether we include that content at the current level or at one level down from the current level depends on the context in which the content is included.
Here is an example in which we completely separate the content from the headings ([example G][7])

`(G) animals_article.tex`

```latex
\documentclass{article}
\usepackage{import}
\usepackage{coseoul}
\title{Animals}

\begin{document}
\maketitle
This is an article about animals.

\levelstay{Octopuses}
\subimport*{octopuses/}{octopus_quote}
\leveldown{Circulatory System}
\subimport*{octopuses/}{circulation_content}
\levelstay{Camouflage}
\subimport*{octopuses/}{camouflage_content}

\levelup{Horses}
This chapter is about horses.

\end{document}
```

`(G) octopuses/octopuses_article.tex`

```latex
\documentclass{article}
\usepackage{import}
\usepackage{coseoul}
\title{Octopuses}

\begin{document}
\maketitle
\subimport*{./}{octopuses_content}
\end{document}
```

`(G) octopuses/octopuses_content.tex`

```latex
\subimport*{./}{octopus_quote}

\levelstay{Circulatory system}
\subimport*{./}{circulation_content}

\levelstay{Camouflage}
\subimport*{./}{camouflage_content}
```

`(G) octopuses/circulation_content.tex`

```latex
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.
```

`(G) octopuses/camouflage_content.tex`

```latex
Octopuses can change color.
They even change the texture of their skin.
```

Example G works, but it's a disaster.
We had to write the outline of the Octopus part of the document twice: one time in `octopuses/octopuses_content.tex` and again in the body of `animals_article.tex`.<sup>4</sup>
Note also that we had to use `\levelup` for the Horse section to account for the fact that upon leaving the octopus parts, we were one level below where we wanted to be.
This illustrates the deep problem with `coseoul`: we have to bring *all* of the headings to the top level file because `coseoul` offers no way to *encapsulate* heading depth.
In other words, because the `currentlevel` counter is global (like all LaTeX counters) we cannot import any files which use `\level(stay)(up)(down)` because they leave the counter at an unknown value.

## Fix `coseoul`: our own macro

Now we come to the final part of this journal entry in which we add the feature `coseoul` lacks and acheive LaTeX nirvanna.
We want a macro that allows us to import an entire document fragment all at once without having to write multiple versios of the headig structure and without having to worry about the value of a counter before and after the imported section.
Let's name this hypothetical macro  `\subimportlevel{dir}{file}` where the `dir` and `file` arguments are exactly the same ones as we woud pass to `\subimport*`.
We want `\subimportlevel` to work like this ([example H][8]):

`(H) octopuses/octopuses_article.tex`

```latex
\documentclass{article}
\usepackage{import}
\usepackage{coseoul}
\input{../macros}
\title{Octopuses}

\begin{document}
\maketitle
\subimportlevel{./}{octopuses_content}
\end{document}
```

`(H) octopuses/octopuses_content.tex`

```latex
\subimport*{./}{octopus_quote}

\levelstay{Circulatory system}
Octopuses have three hearts: one for each set of gills and another systemic one.
Their blood uses copper to bind oxygen, so it's greenish blue.

\levelstay{Camouflage}
Octopuses can change color.
They even change the texture of their skin.
```

`(H) animals_article.tex`

```
\documentclass{article}
\usepackage{import}
\usepackage{coseoul}
\input{macros}
\title{Animals}

\begin{document}
\maketitle
This is an article about animals.

\levelstay{Octopuses}
\subimportlevel{octopuses/}{octopuses_content}

\levelstay{Horses}
This chapter is about horses.

\end{document}
```

`(H) macros.tex`

```latex
% our \subimportlevel macro goes here
```

All we have to do now is figure out how to write the `\subimportlevel` macro, and put it in `macros.tex`.
Here's a speudocode outline

```latex
\newcommand{\subimportlevel}[2]{ % arguments are dir, file
  temp = value of the currentlevel counter  % this line is tricky
  currentlevel -= 1  %-1 means one level deeper
  \subimport*{#1}{#2}
  currentlevel = temp
}
```

Remember at the beginning when I said that LaTeX is not suited to logic?
Well I meant it, and in turning this pseudocode into working LaTeX we'll see why.
The hard part is `temp = value of the currentlevel counter`.
Variables in LaTeX are always global, so if the imported file uses our macro, then `temp` gets mutated and its value after the `\subimport` command depends on the contents of the imported file.
However, we can protect `temp` using a group:

```latex
\newcommand{\subimportlevel}[2]{     % 1
  \edef\temp{\thecurrentlevel}       % 2
  \bgroup                            % 3a
  \addtocounter{currentlevel}{-1}    % 4
  \subimport*{#1}{#2}                % 5
  \egroup                            % 3b
  \setcounter{currentlevel}{\temp}   % 6
}
```

Here's a breakdown of how this macro works:

1. Define a new command, called `\subimportlevel`, which takes the directory and filename as two arguments.
The values of these arguments are accessed via `#1` and `#2`.

2. Define `\temp` *after expanding* `\thecurrentlevel`.
See [this LaTeX Stack Exchange post](http://tex.stackexchange.com/questions/8163/what-is-the-difference-between-let-and-edef) for details of how `\edef` works.
Note that in LaTeX, `\theXYZ` is the current value of counter `XYZ`.

3. Define the start and end of a group, which protects `\temp` from being mutated across the group boundary.

4. Decrement the `currentlevel` counter, taking us one level deeper.

5. Import the file we want.

6. Set `currentlevel` back to the value it had before the import.

To see it work, download [example H][8], drop the above code into `macros.tex`, and try compiling both `octopuses/octopuses_article.tex` and `animals_article.tex`.
You'll see that they work as intended!

We could call it quits here, but there's one little thing we could do better.
In example H, we used a group to protect the value of `\temp`.
Using a group to protect a variable could lead to unexpected behavior.
Groups are used for various environments, such as equations, and aren't really intended to be used for sectioning.
It's conceivable that our use of groups to protect `temp` could interact poorly with code in another package.
Now I admit, I haven't actually encountered a problem with the way we defined `\subimportlevel`, but it's not that hard to rewrite it without using a group.
Instead, we'll store the value of `currentlevel` in a different macro every time `\subimportlevel` is invoked:

```latex
\makeatletter
\newcounter{subimportleveldepth}                                                             % 1a
\setcounter{subimportleveldepth}{0}                                                          % 1b
\newcommand{\subimportlevel}[2]{                                                             % 2
  \expandafter\edef\csname @currentlevel\thesubimportleveldepth\endcsname{\thecurrentlevel}  % 3
  \addtocounter{subimportleveldepth}{1}                                                      % 4
  \addtocounter{currentlevel}{-1}                                                            % 5
  \subimport*{#1}{#2}                                                                        % 6
  \addtocounter{subimportleveldepth}{-1}                                                     % 7
  \setcounter{currentlevel}{\csname @currentlevel\thesubimportleveldepth\endcsname}          % 8
}
\makeatother
```

1. Make a new counter called `subimportleveldepth` and initialize it to 0.
This counter keeps track of how many times we recursively call `\subimportlevel`

2. Define the `\subimportlevel` macro, taking two arguments, just like before.

3. Define a new macro named `@currentlevelX` whose value is `Y`, where `X` is the value of `subimportleveldepth` and `Y` is the value of `currentlevel`.
Therefore, we've "saved" the value of `currentlevel` in a uniquely named macro.

4. Increment the value of `subimportleveldepth` so that subsequent uses of `subimportlevel` do not overwrite the macro we defined in step 3.

5. Decrement the `currentlevel` counter, taking us one level deeper.

6. Import the file we want.

7. Decrement the value of `subimportleveldepth`, therefore freeing up macro names to use on subsequent calls to `\subimportlevel`.
This is safe now because we're done with any `@currentlevelX` macros defined while processing the imported file.

8. Set `currentlevel` back to the value we saved in step 3.

Now we're really done.
I use this version of `\subimportlevel` in my work, and it's great.

## Footnotes

1: See, for example, [LuaTeX](http://www.luatex.org/).

2: By the way, `\includegraphics` has the same problem.

3: `coseoul` stands for **co**ntext **se**nsitive **ou**t**l**ine elements.

4: Of course, we could factor the octopus stuff out of the body of `animals_article.tex`, but the point is that we have to write two versions of it.

[1]: {{ site.url }}/download/tex-modularity/example-A.zip
[2]: {{ site.url }}/download/tex-modularity/example-B.zip
[3]: {{ site.url }}/download/tex-modularity/example-C.zip
[4]: {{ site.url }}/download/tex-modularity/example-D.zip
[5]: {{ site.url }}/download/tex-modularity/example-E.zip
[6]: {{ site.url }}/download/tex-modularity/example-F.zip
[7]: {{ site.url }}/download/tex-modularity/example-G.zip
[8]: {{ site.url }}/download/tex-modularity/example-H.zip

