all: build/paper.pdf

build/paper.pdf: main.tex | build
	lualatex --output-directory=build main.tex

main.tex: header.tex lit.bib content/*

build:
	mkdir -p build

# graphics:
# 	mkdir -p graphics

clean:
	rm -rf build

.PHONY: all clean