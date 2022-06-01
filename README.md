# 20xx-master-template

## Guidelines

### Chapters - Sections - Subsections

Make sure to use the provided commands for chapters, sections, and subsections:

```latex
\chapter{}      % New chapter
\label{chap:}    % Prefix your label with 'sec:'

\section{}      % New section
\label{sec:}    % Prefix your label with 'sec:'

\subsection{}   % New sub section
\label{sec:}    % Prefix your label with 'sec:'
```

Whenever there is a reference to a logical structure of your document, the name of the structure must be capitalized and followed by the full number of the section (e.g., `in Chapter 1`). This can be achieve by writing `in Chapter \ref{chap:introduction}`.

References to chapters, sections, and subsections should follow this schema:

| structure     | naming convention | reference                 |
|---------------|-------------------|---------------------------|         
| chapter       | Chapter           | [...] in Chapter 1        |
| section       | Section           | [...] in Section 1.1      |
| subsection    | Section           | [...] in Section 1.1.1    |
| subsubsection | Section           | [...] in Section 1.1.1.1  |

Please avoid using `subsubsection` if not strictly necessary.

#### Numbering

The numbering of logical structures follows this schema:
`chapNumber`.`secNumber`.`subsecNumber`.`subsubsecNumber`

Figures, Tables, Listings, should always be numbered per *chapter*.

#### Using \autoref{}

You can use the command `\autoref{}` instead of writing `in Chapter \ref{chap:introduction}` or `in Section \ref{sec:example}`
This command can automatically detect which logical structure is referencing an creates the reference accordingly.

Autoref needs to be configures, i.e.:

```latex
\addto\captionsenglish{%
  \def\chaptername{Chapter}%
  \def\sectionname{Section}%
  \def\subsectionname{Section}%
}

\addto\extrasenglish{%
  \def\chapterautorefname{Chapter}%
  \def\sectionautorefname{Section}%
  \def\subsectionautorefname{Section}%
}
```

### Common Style Tips

#### Acronyms

The first time an acronym occours write the extended name followed by the acronym in parenthesis, e.g. `Organizzazione delle Nazioni Unite (ONU)`. In the rest of the document you will write the acronym.

*Note*: the abstract is not part of the main body of your document. If an acronym appears in the abstract, the first time it appears your should write it in its extended form. Then in the main body of your document you will repeat this process.

#### Abstract

In the abstract avoid using:
  - references
  - citations

#### Emphasis: Bold or Italics?

Avoid using `\textbf{}` (**bold**) if you need to emphatize a word. You should use `\textit{}` (*italics*).

#### Terms in another language

Use `\textit{}` (*italics*) for foreigner terms, e.g., `My kid is going to \textit{scuola media}`.

Do not use `\textit{}` (*italics*) for terms commonly used in english, e.g., `I have a dejà vu`.

### Citations

All citations must be followed by a reference to the corresponding source (i.e., \cite{}).


#### Quotations

Short quotations (1-2 lines), should be integrates in the text with quotes, e.g.:

```latex
Gallidabino et al. defines this guideline as ``very long and hopefully useful'' \cite{gallidabino2022}.
```

Long quotations (2+ lines), should define their own quotation environment, e.g.:

```latex
\usepackage{csquotes}

Andrea Gallidabino et al. claimed in his thesis \cite{gallidabino2020}:
\begin{displayquote}
[...]
\end{displayquote}
```

### Figures and Floats

Avoid using the float `h` (i.e., `here`).
You are ncouraged to used floats `t` (i.e., `top`) and if necessary `b` (i.e., `bottom`).

You should add your `figure` environment *immidiately after* the paragraph that references it. Latex layouting will internally decide a *good* place to insert your figure. You can override Latex decision by prefixing the float with a bang `!` (e.g., `!t`, `!b`).

If your figure is displayed on a page you do not expect check the *Tricks* section.

```latex
\begin{figure}[t]                        
  \centering                              % Centers the content of the environment (in this case 'figure')
  \includegraphics[width=\linewidth]{}    % Please organize your project, do not include images directly from the root (e.g., create folder 'figures')
\end{figure}
```

### Captions and References

  The captions of `Tables` and `Listings` should be included on top.
  
  Captions of Figures and other logical stuctures should be included on the bottom.

  - Figures:
    ```latex
    \begin{figure}[t]                         
      \centering                              
      \includegraphics[width=\linewidth]{}    
      \caption{}                              % Caption goes after 'includegraphics'
      \label{fig:}                            % Prefix your label with 'fig:'
    \end{figure}
    ```
    
  - Figures and SubFigures

    ```latex
    \usepackage{subcaption}

    \begin{figure}[t]
      \centering

      \begin{subfigure}[t]{0.4\textwidth}       % Width of the subfigure
        \centering
        \includegraphics[width=\linewidth]{}
        \caption{}                              % Caption of the subfigure
        \label{fig:}		
      \end{subfigure}
      % WARNING: If you leave an empty line in here images will not be displayed on the same line (new paragraph)
      % You are encourage to use '\hfill' here
      \begin{subfigure}[t]{0.4\textwidth}       % Width of the subfigure
        \centering
        \includegraphics[width=\linewidth]{}
        \caption{}                              % Caption of the subfigure
        \label{fig:}
      \end{subfigure}

      \caption{}                                % Make sure to have a caption for the whole figure
      \label{fig:}
    \end{figure}
    ```
    
  - Tables:

    ```latex
    \begin{table}[t]                            % Avoid using float 'h' (here), you are encouraged to use 't' (top) or 'b' (bottom)
      \caption{}                                % Caption goes before 'tabular' environment
      \label{tab:}                              % Prefix your label with 'tab:' 
      \begin{tabular}{}
      \end{tabular}
    \end{table}
    ```
    
    
## Tricks

### Float appears at the end of the document / Float is too big

*Possible problem*:

Latex is not able to find a good position for your floats because its width is bigger than the `\textwidth` of your document or it is too long.
In this case all subsequent floats are moved at the end of your document.

*Solutions*:
  - Set the width of the float to \textwidth
  - Set the height of the float to \textheight

**Floats do not appear on the page I reference them, but some page later**

*Possible problem*:

Usually this is a symptom that you have too many figures and too few words explaining them.

*Solutions*:
  
  - Write more text explaining the images
  - Remove some images
  - If you are 100% sure that you need all the images and you do not need to write more text, you can flush all images on a page using this command `\afterpage{\clearpage}`.
    This command inserts a new page after the current page is full, meaning that all floats that need to be inserted can be inserted in this new page.
