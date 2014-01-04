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

Download this branch and extract it.

*The Syntax Highlighting*:

Put the _sourceview-3.0_ folder inside */home/_your-username_/.local/share/*

*The Snippets*:

Within Gedit, enable the _Snippets Completion_ plugin.
Go to Tools >> Manage Snippets
Click on the _Import Snippets_ button, select the _snippets.xml_ file and confirm.

*Running Sketches within Gedit*:

Within Gedit, go to plugins and enable _External Tools_.
Go to Tools >> Manage External Tools
Add a new entry with the following code:

		#!/bin/sh
		processing-java --sketch=$GEDIT_CURRENT_DOCUMENT_DIR --output=$GEDIT_CURRENT_DOCUMENT_DIR/run --run --force

Note that if you have processing-java installed in a different folder than your system's default, you will need to change the script to:

		#!/bin/sh
		/path_to_processings_folder/processing-java --sketch=$GEDIT_CURRENT_DOCUMENT_DIR --output=$GEDIT_CURRENT_DOCUMENT_DIR/run --run --force

*Auto-Formating*:

_Note that this requires you to have Vim installed in your system._

Go to Tools >> Manage External Tools
Add a new entry with the following code:

		#!/bin/sh
		CMD_FILE_NAME=.formatcommand;
		TMP_FILE_NAME=.tempvimfile;
		touch $CMD_FILE_NAME&&echo "gg=G :wq! "$TMP_FILE_NAME > $CMD_FILE_NAME&&(vim $GEDIT_CURRENT_DOCUMENT_NAME -s $CMD_FILE_NAME > /dev/null 2>/dev/null)&&rm $CMD_FILE_NAME;
		cat $TMP_FILE_NAME
		rm $TMP_FILE_NAME
	
Set _Save_ to _Current Document_
Set _Entry_ to _Nothing_
Set _Output_ to _Replace Current Document_

You might have to save before running it as it uses the saved file in the drive as source and for some users the plugin fails to save.

---

###How do I use the snippet completion?
Gedit's snippet completion works like this: you type the shortform and press tab, it will create the entire snippet. For instance, using my snippets, if you type

		rec
		
And hit tab, it will turn into:

		rect();
		
With the caret within the parenthesis so that you can type the attributes you want.
To see all the currently available snippets, go to the Snippet Manager.

---

###Why haven't you added the commas and whatnot?
I had it earlier that the output for the operation above was:

		rect($1,$2,$3,$4);$0
		
What this did was make it so you just had to tab between parameters. It might sound great at first but Gedit can act erraticly, specially when we have things like mouseX also possible to complete with tab. Instead of:

		rect(mouseX, mouseY, width,height);
		
If I tried to input a snippet within the first parameter I would get:

		rect(mouseX
		
Due to this weird behavior, I thought it would be easier to type in the commas than to backtrack all the time.

###I think something could be made a lot better than what you currently have!
By all means, feel free to either fork this or submit patches, I'm all ears. :)
