---
layout: post
published: true
title: Keyboard navigation in Sublime Text for column layouts
date: '2014-05-25 10:40:20 +0100'
categories:
  - Sublime-Text
---

A year or so ago I switched from an IDE to Sublime Text for web development. During that time I have had urges to switch to Vim, which was the inspiration for Sublime. The main reason for this is to enourage me to use keyboard shortcuts for everything. I will probably never make that switch, I'm too lazy, so I suppose I should learn the Sublime shortcuts that still cause me to reach for the mouse.

First up we have managing column layouts using keyboard shortcuts. Since I generally use a massive 27 inch screen for coding I like to have two, or sometimes three files visible in column layout, in my Sublime window.

Now for the exercises.

*   First open an existing project that you have. Open a few files, using **cmd-p** to locate them. You should now have one column/viewport with several files open in it.
*   Try switching between them. Use **cmd-opt-(left/right arrow)**
*   Let's open up a new viewport. For a second column that would be **cmd-opt-2** (where 2 is the number of columns, try 3 or 4).
*   Now you should have a few files in the first column and a new file in the second. Ignore this new file, sublime has not saved this anywhere and we want to move one of our existing files over here. However, your cursor is at the top of this new file and we do not want to do anything with this, so try moving the cursor back to a previous file using **cmd-opt-(left/right arrow)**. Even better you can use **ctrl-1** or **ctrl-2** to switch the cursor to the first or second column view.
*   Nove this file into your empty second view, use **ctrl-shift-2** (where 2 is again the pane number).

Post-it to stick on my monitor:

*   **cmd-opt-(left/right arrow)** Cycle files.
*   **ctrl-#** Switch to column pane number.
*   **cmd-opt-#** Create number of column panes.
*   **ctrl-shift-#** Move current file to pane number.

That's easy, right? Now I need to force myself to use this, rather than reaching for the mouse. If you find learning keyboard shortcuts time consuming your might find the [CheatSheet app](http://www.mediaatelier.com/CheatSheet/ "CheatSheet") useful.
