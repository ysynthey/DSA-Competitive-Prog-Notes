# DSA & Competitive Programming Notes in C++ - ySynthey

Welcome to my public repository for Data Structures, Algorithms (DSA), and Competitive Programming! These notes are a collection of my personal implementations and logic breakdowns, shared publicly because sharing is caring.

## Project Goal
The objective of this repository is to document efficient problem-solving strategies and algorithm implementations in C++. It serves as both a personal reference and a resource for anyone learning technical computing.
I write explanations and comments based on how I see them, I like to use examples as plain text as the jargon being thrown around in other references are too intimidating and aren't properly explained. Learning shouldn't be made difficult on oneself by static means.
Also at the time of creating this repo, I am taking DSA in University and I think it would be very embarassing if I were to not excel in it.

## Table of Contents - Continuously Updating
The notes are categorized by their type (Is it about Trees or Linked Lists?) and their time complexities (both in folders) to make it easier to find specific algorithms based on what you're currently interested in.

Click to be directed to a topic!

# Sorting

### O(n²) -  Quadratic
* **[Bubble Sort](./Sorting/O(n%5E2)/Bubble.md):** A simple comparison-based sort that bubbles the largest elements to the top.
* **[Selection Sort](./Sorting/O(n%5E2)/Selection.md):** Systematic scanning to find the minimum value and swapping it once per pass.
* **[Insertion Sort](./Sorting/O(n%5E2)/Insertion.md):** Shifting elements to create gaps and inserting a key value (like sorting books on a shelf).

### O(log n) - Logarithmic
* **[Binary Search](.Searching/O(log%20n)/Binary%20Search.md):** Continuously divide your array/vector by half until you find your target.
###  O(n log n) - Linear Logarithmic
* **[Merge Sort](./O(n%20log%20n)/Merge.md):** A "Divide and Conquer" strategy that splits arrays recursively and merges them back up already sorted in whatever order you want.

### Searching

### O(n²) -  Quadratic
Binary Search

# Data Structures

* **[Linked Lists](<Data Structures/Linked Lists.md>):** A much more dynamic approach to handling several data in several places than arrays, they allow for easy operations such as inserting/deleting/outputting data and allocate space for certain data in several places in memory on the fly in their assigned Nodes. connecting them through a system of pointers. Highly applicable to several games and software as traversal/reversal of linked lists allow access to perhaps, the previous or next page in a shopping website for example.

## What to expect?
Each file follows a consistent format:
1. **Name & Language:** Clear identification of the algorithm and what language to be used.
2. **Complexity:** Big O notation for time complexity.
3. **Overview:** Straight-to-the-point explanation on what something is from my own understanding.
4. **Supporting Detail:** Real-life analogies and logic breakdowns. (Haven't added for all)
5. **Implementation:** Hopefully clean C++ code with detailed comments. Please go easy on me, I'm still (and always am) learning!

---
*Disclaimer, since I value truth: Google Gemini usually makes most of the md (markdowns), the code implementations and explanations are 100% human made.*
