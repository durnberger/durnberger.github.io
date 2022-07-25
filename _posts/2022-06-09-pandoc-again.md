---
layout: post
categories: linux
tags: [bash, pandoc, pdf, weasyprint]

---

Using pandoc and weasyprint to create a letter template, but this time a little more elegantly!

<!--more-->

In an earlier post, [Pandoc](/2022/05/05/pandoc){:target="_blank"}, I created a bash script to convert a `markdown` file to a `pdf`. The final version converted all markdown files within a defined folder.

Using the script shown below, a list of markdown documents is displayed. You can then select one of those documents for conversion. The rest would remain untouched.

The key is these 2 lines;

```
files="$(ls --file-type *.md)"

select filename in ${files};
```

The first line lists the markdown files in the given directory, whilst the second line allow you to select one file from the list, and for that file to be processed.

Much neater!

```
#!/bin/bash
#
# ~/bin/write2pdf.sh
#
# With thanks to:
# https://linuxconfig.org/how-to-create-a-selection-menu-using-the-select-statement-in-bash-shell
#

cd /home/$USER/Correspondence

# Choose from letter, memo or note
#
echo "Are you writing a letter, memo or note?"
echo "1) Letter"
echo "2) Memo"
echo "3) Note"
read choice


if [ "$choice" == "1" ]; then
# Letter

	PS3="Select a file:"

	files="$(ls --file-type *.md)"

	select filename in ${files};

		do

		stem=$(basename ${filename} .md)

		pandoc -f markdown --include-before-body layout/header-letter.html --include-after-body layout/footer.html --metadata pagetitle="$stem" --metadata lang="en-GB" --pdf-engine weasyprint --css style/style.css ${filename} -o $stem.pdf

			break;

		done
# End of letter




elif [ "$choice" == "2" ]; then
# Memo

	PS3="Select a file:"

	files="$(ls --file-type *.md)"

	select filename in ${files};

		do

		stem=$(basename ${filename} .md)

		pandoc -f markdown --include-before-body layout/header-memo.html --include-after-body layout/footer.html --metadata pagetitle="$stem" --metadata lang="en-GB" --pdf-engine weasyprint --css style/style.css ${filename} -o $stem.pdf

			break;

		done
# End of memo



else
# Note
	PS3="Select a file:"

	files="$(ls --file-type *.md)"

	select filename in ${files};

		do

		stem=$(basename ${filename} .md)

		pandoc -f markdown --include-before-body layout/header-note.html --include-after-body layout/footer.html --metadata pagetitle="$stem" --metadata lang="en-GB" --pdf-engine weasyprint --css style/style.css ${filename} -o $stem.pdf

			break;

		done
# End of note

fi
```

With thanks to [Linuxconfig.org](https://linuxconfig.org/how-to-create-a-selection-menu-using-the-select-statement-in-bash-shell){:target="_blank"} for setting me on the right track.
