# Fast Library Identification and Recognition Technology (FLIRT) Signature File Database

## What is FLIRT?
Fast Library Identification and Recognition Technology, also known as FLIRT, is IDA's internal symbols identifier that searches through disassembled binaries in order to locate, rename, and highlight known library subroutines. FLIRT elimates the need to analyze functions that could be understood simply by reading documentation or source code from the library it came from and reduces the amount of work required in order to reverse and understand symbol-stripped binaries by a considerable amount.

For more information visit: https://www.hex-rays.com/products/ida/tech/flirt/index.shtml

## How does FLIRT work?
Here's an oversimplified diagram on FLIRT's internal workings:

![alt text](https://i.imgur.com/28YPsqM.png "FLIRT Internals Diagram")

The input to the system is a library file (.lib on Windows) from a library of choice while the output is a signature file (.sig) stored under <IDADIR>/sig (and only there or else IDA won't find it). Using one of the tools (plb/pcf/pelf) (provided [here](https://www.hex-rays.com/products/ida/support/ida/flair695.zip) for paying customers) you convert all the functions in the library to signatures stored in a PAT file (.pat). The final stage in creating a signature file involves converting the generated PAT file into a .sig file usable by IDA with the use of sigmake. The problem with this is that sometimes collisions will exist for signatures since the method Hex-Rays uses is not fool proof. When an error occurs an EXC (.exc) file is created. In order to ignore collisions, simply edit this file by removing the first few comments (lines that start with ';') and re-run sigmake.

For more information look inside the readme inside the FLAIR tools directory.

## What is this repository for?
Considering the fact that there are countless libraries out there (both open/closed source) each with their endless builds/versions, it's obvious that the Hex-Rays team cannot always provide us with the signature files we need. Due to this, I've created this repository in hopes of it serving as a hub for reverse engineers to grab signature files from (and hopefully upload too).

## How can I contribute?
Anyone can contribute to this repository by generating a signature file for a specific version of a library (or several!) and following the rules under [ethics](#ethics).

## Ethics
Due to the fact that there are various libraries/versions to manage, it's a requirement that we sort all the info in the easiest possible way so that people can find what they're looking for with ease. Simply follow the rules below and hopefully everything will run smoothly:

1. Make sure to ignore conflicting names when using sigmake
2. Always submit the signature file, the EXC file (if there are conflicting signatures), and also that pattern file
3. Organize your submission in the standard folder structure (library/os)
5. Add a descriptive name to your signature files using the -n option in sigmake
6. Before committing, make sure that signatures for your library and version hasn't been submitted
7. _Do not_ submit the library file itself due to copyright/redistribution issues

## Author
Michael "Maktm" A.
