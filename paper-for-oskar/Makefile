# all: build/main.pdf

# build/main.pdf: main.tex content/* | build
# 	TEXINPUTS=build: \
# 	  BIBINPUTS=build: \
# 	  max_print_line=1048576 \
# 	latexmk \
# 	  --lualatex \
# 	  --output-directory=build \
# 	  --interaction=nonstopmode \
# 	  --halt-on-error \
# 	main.tex

# main.tex: header.tex lit.bib content/* graphics/*

# build:
# 	mkdir -p build

# graphics:
# 	mkdir -p graphics

# clean:
# 	rm -rf build

# .PHONY: all clean

ifeq (,$(shell sh -c 'cygpath --version 2> /dev/null'))
  # Unix
  pwd := $$(pwd)
  translate = $1
else
  # Windows mit MSys2/Cygwin
  pwd := $$(cygpath -m "$$(pwd)")
  translate = $(shell echo '$1' | sed 's/:/;/g')
endif

# Farben/ Textformatierung
BACKGR=`tput setaf 0`
GREEN=`tput setaf 10`
GREENB=`tput setab 10`
BOLD=`tput bold`
RESET=`tput sgr0`
now:=$(shell date +"%m-%d-%I-%M")

all: paper$(now).pdf

again:
				@make clean
				@make all

clean:
				@rm -rf build
				@echo ${GREEN}${BOLD}Removing build folder${RESET}


build:
				mkdir -p build

data:
				mkdir -p data


graphics:
				mkdir -p graphics

paper$(now).pdf: main.tex content/* header.tex lit.bib graphics | build
				@TEXINPUTS="$(call translate,build:)" lualatex \
								--output-directory=build \
								--interaction=nonstopmode \
								--halt-on-error \
				main.tex|grep -B 12 -e'no output PDF file produced' -e'LuaTeX' --color=auto
				@echo
				@BIBINPUTS=build: biber build/main.bcf|grep -i -e'biber' -e'error' -e'errors' -e'warn' -e'warnings' --color=auto
				@echo
				@lualatex \
								--output-directory=build \
								--interaction=nonstopmode \
								--halt-on-error \
				main.tex>/dev/null
				@lualatex \
								--output-directory=build \
								--interaction=nonstopmode \
								--halt-on-error \
				main.tex|grep  -e'reference' -e'LuaTeX' --color=auto
				@mv -T build/main.pdf /mnt/g/My\ Drive/Research\ Paper\ Versions/paper$(now).pdf

				@make clean
				@echo ${GREENB}${BACKGR}Success!${RESET}
