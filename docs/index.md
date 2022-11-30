---
layout: default
---

<table>
<colgroup>
  <col width="25%" />
  <col width="25%" />
  <col width="25%" />
  <col width="25%" />
</colgroup>
<thead>
<tr class="header">
  <th style="text-align: center">rivt (API)</th>
  <th style="text-align: center">rivtCalc (installers)</th>
  <th style="text-align: center">rivtDocs</th></tr>
  <th style="text-align: center">rivtManual</th></tr>
</thead>
<tbody>
<tr>
  <td style="text-align: center"><a href="https://github.com/rivtcalc/rivt"> <img src="./assets/img/rivt01a.png" width="60" height="40" /></a></td>
  <td style="text-align: center"><a href="https://github.com/rivtcalc/rivtinstall"> <img src="./assets/img/rivt_install.png" width="60" height="40" /></a></td>
  <td style="text-align: center"><a href="https://rivtdocs.net"> <img src="./assets/img/rivtdoc09.png" width="60" height="40" /></a></td>
  <td style="text-align: center"><a href="https://rivt.info"> <img src="./assets/img/rivtman01.png" width="60" height="40" /></a></td>
</tr>
</tbody>
</table>

## Introduction

Open source software tools will increase sharing and improve productivity if used for general engineering calculations.

Many engineering technologies change slowly. Design procedures become fixed by
legal codes and standards for years at time. This means that good engineering
design work is based on skillful fitting together  of established technologies, rather than developing new technologies or methods.

Calculations establish and convey the reasoning behind the designs and
integration. If they are easy to share and edit, then prior similar designs
become efficient starting points for new designs. An initial calculation
assembled from existing designs can be developed into a final design more
efficiently then starting from scratch. But a calculation tool adapted to
exchange and integration is needed.

Many high-quality calculation programs are in general use. Unfortunately
they include barriers to widespread calculation sharing (see table). Most of
them have high initial and recurring software costs as well as strict
limitations on computing devices. File formats and features often change in a
way that require continual program upgrades or subscriptions. Incompatibility
between the different programs requires multiple software purchases. And
generally they do not produce collated reports or easily allow version control.
These barriers to sharing forces duplicate work, increased errors, reduced
quality, and slower technology transfer.

**Table: Calculation Program Comparison**

<img src="./assets/img/table1.png" width="1000" height="180" />

Through a standard sharing framework the engineering professions have an
opportunity to produce extensive, reusable calculation libraries that can be
recombined in efficient and productive ways for new designs. This model of
shared, incremental improvement using text-based documents is perhaps **the**
major reason behind recent rapid advances in software development and
distribution. The extension of this approach to general engineering
calculations is natural.

## Introduction

## **rivt** 

**rivt** is an open source Python API that minimizes barriers to sharing and
collaboration. It incorporates a lightweight, highly readable markup language
(**rivtText**) Installers are provided for the open source stack and tools
(**rivtCalc**) that facilitate efficient editing and publishing.

The **rivt** API uses file and folder naming conventions to organize and
assemble calcs into collated reports. Folders are shown in bold, user names in
italics and explanatory notes in parenthesis.

- **rivt_*project_name*** 
    - .vscode **(VSCode settings)**
    - **calcs**
        - **rv00** **(calc configuration data)**
            - units.py
            - pdf.sty
            - html.css
        - **rv01*_calc_division_name1***  **(division name for report**)
            - **rv0101_calc_name1**
                - rv0101_*calc_name1*.py **(input file)**
                - *chart1*.csv **(csv resource)**
                - *functions1*.py **(functions resource)**
                - *paragraph1*.txt **(text file resource)**
                - README.txt **(calc output)**
            - **rv0102_calc_name2**
                - rv0102_*calc_name2*.py
                - *functions2*.py
                - README.txt
         - **rv02*_calc_division_name2***
            - **rv0201_calc_name3**
                - rv0201_*calc_name3*.py 
                - *paragraph2*.txt
                - README.txt 
            - **rv0202_calc_name4**
                - rv0102_*calc_name4*.py
                - *functions3*.py
                - README.txt
   - **docs**
        - **d00** **(project and report configuration data)**
            - report.txt
            - *pdf_style*.sty
            - *project_data*.xlsx
        - **d01** **(corresponds to the division calc folder)**
            - *image1*.jpg
        - **d02**
            - *image2*.jpg
            - *attachment*.pdf    
    - **reports** **(PDF output)**
        - d0101_*calc_name1*.pdf
        - d0102_*calc_name2*.pdf
        - d0201_*calc_name3*.pdf
        - d0202_*calc_name4*.pdf
        - *report*.pdf
    - **sites** **(HTML output)**
        - **resources**
            - *image1*.png
            - *image2*.png
        - index.html
        - d0101_*calc_name1*.html
        - d0102_*calc_name2*.html
        - d0201_*calc_name3*.html
        - d0202_*calc_name4*.html
            
The **rivt_** prefix for the project folder and the four top-level folder names
(*calcs, docs, reports and sites*) are required. The file prefix is used to
organize a report and has the form rvddnn_*filename*.py, where dd is the
division number and ddnn is the calc number. The rest of the file name is a
user chosen label.

The API is designed so that only the **calcs** folder is shared. The folder
includes all of the calculation, except for binary and proprietary files such
as images, PDF attachments and client data. They are stored in the **docs**
folder.

A typical project flow includes:

1. Search **Github** README files using the primary
search term **rivt**, plus additional specific terms. Since each calc output is written to the README file, the search is full text. 
2. Clone the repo of interest 
3. Combine and edit calcs for the new project.
4. Create a public repo for the new calc folder.  

```
                +-------------------------+
                |     Edit and run rivt   | 
                |         as file or      |
                |     interactive cells.  |
                +-----------||------------+
+-------------+ +-----------||------------+  
|  Write cell | |   interactive IDE?      | 
|  output to  | |  (VSCode, Pyzo, etc.)   |
|  terminal   <=== YES       NO           |  
+------+------+ +-----------||------------+  
       |        +===========||============+      
       |        |    Write calc files:    |        
       +========>     utf-8, reST, TeX    |          
                +===========||============+
+=============+ +-----------||------------+
| Write doc   | |                         | +------+
| files:      | |       Write docs?       | | End  |
| HTML, PDF   <=== YES                 NO ==>      |
+======+======+ +-------------------------+ +------+
       |        +-------------------------+ +------+
       |        |      Write report?      | | End  |
       +========>           YES        NO ==>      |
                +-----------||------------+ +------+
                +===========||============+
                |    Write PDF or HTML    |
                |       report file       |
                +=========================+

```

## rivtText

The **rivt** API includes five methods: R(rs), I(rs), V(rs), T(rs), X(rs). The
argument rs is a triple quoted Python string containing **rivtText** commands and
tags.

**rivtText** was designed for simplicity and readability. It includes commands,
tags, reStructuredText (reST) markup and native Python code. **rivt** strings
are interpreted line by line. Lines that begin with **||** process external data
files. Lines that terminate with **[tag]_** format output. Tags that end in double
underscore **[tag]__** format blocks of text.

In interactive mode using an IDE (e.g. VSCode), each API call can be called
separately using the cell tag (#%%) in the preceding line. Cells can be
evaluated one at a time and the output (utf8) displayed interactively. 

In file execution mode the entire input file is executed and the formatted
calculation is written to disk as a calc (utf8) or doc (PDF or HTML). **rivt**
input files are Python files and calcs are text files. Doc files also include
project specific and copyrighted information (clients, images etc), which are
typically not shared in the generic text input and output files.

The rivtText syntax is defined in the documentation: [**link to rivtDocs**](https://github.com/rivtcalc/rivtdocs)
    
## rivtCalc

**rivtcalc** is an open source software stack for writing calculation
documents. It defines a default installation that includes **rivt**,
**VSCode**, **LaTeX** and **Github**. **rivt** is the Python library and API
that processes **rivtText**. **VSCode** and **Github** are the extensible,
customizable editor and searchable repository from Microsoft.

**rivtcalc** can be installed on the desktop or mobile devices, or run remotely
in the cloud. The minimum software needed to process a **rivt** calc is Python
3.8 (or higher), Python libraries and a plain text processor (text output
only). The minimum implementation can be explored online at 
[**link to repl.it**](https://repl.it)

For efficient workflow and formal document production the standard **rivt**
installation requires: 

1. Python 3.8 or above + libraries
2. VSCode + extensions
3. LaTeX 
4. Github account

**rivtcalc** installers are available for every OS platforms and **rivt** can
be run in the cloud (e.g. Codespaces). Installation programs are provided here:
[**link to rivt**](https://github.com/rivtcalc/rivtinstall)

**rivt** may be run in a number of different ways:

1. Local install (all desktop OS). The installer does a system install of
   - Python 3.8 with science and engineering libraries
   - VSCode xxxx with extensions
   - TexLive 2022
2. Zip file (Windows only).  
    - The zip file unzips to  single folder, that may be copied
    anywhere, and includes portable versions of the following:
      - Python 3.8 with science and engineering libraries
      - VSCode xxxx with extensions
      - TexLive 2022
3. Github Codespace
      - clone the environment into your repository from here --------


