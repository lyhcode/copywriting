topdf:
	pandoc --template=default.latex --latex-engine=xelatex -V fontsize=13pt part1.txt -o part1.pdf
	pandoc --template=default.latex --latex-engine=xelatex -V fontsize=13pt part2.txt -o part2.pdf
	pandoc --template=default.latex --latex-engine=xelatex -V fontsize=13pt part3.txt -o part3.pdf
	zip -r ../ireport.zip part1* part2* part3* author*
