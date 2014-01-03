#gedit-processing

A set of files and configurations to enable gedit as a Processing IDE.

---

###That sound great but what is included?
- Syntax Highlighting (automatic when editing .pde files)
- Running a sketch straight from Gedit
- Auto-Formatting
- Snippet completion
---
###How do I install it?
Information still pending.


---

###How do I use the snippet completion?
Gedit's snippet completion works like this: you type the shortform and press tab, it will create the entire snippet. For instance, using my snippets, if you type
		rec
And hit tab, it will turn into:
		rect();
With the caret within the parenthesis so that you can type the attributes you want.

---

###Why haven't you added the commas and whatnot?
I had it earlier that the output for the operation above was:
		rect($1,$2,$3,$4);$0
What this did was make it so you just had to tab between parameters. It might sound great at first but Gedit can act erraticly, specially when we have things like mouseX also possible to complete with tab. Instead of:
		rect(mouseX, mouseY, width,height);
I would get:
		rect(mouseX
Due to this weird behavior, I thought it would be easier to type in the commas than to backtrack all the time.