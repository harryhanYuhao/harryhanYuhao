.PHONY: all clean

all:
	latexmk main.tex --pdf
	mv main.pdf CV_HarryHan.pdf
	latexmk -c
	rm -f *.gz

clean:
	latexmk -c
	rm -f *.gz
