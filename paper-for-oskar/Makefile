all: build/main.pdf

build/main.pdf: main.tex content/* | build
	TEXINPUTS=build: \
	  BIBINPUTS=build: \
	  max_print_line=1048576 \
	latexmk \
	  --lualatex \
	  --output-directory=build \
	  --interaction=nonstopmode \
	  --halt-on-error \
	main.tex

main.tex: header.tex lit.bib content/* graphics/*

build:
	mkdir -p build

graphics:
	mkdir -p graphics

clean:
	rm -rf build

.PHONY: all clean
