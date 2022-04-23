name=diploma
main=diploma

FILES=$(main).tex $(main).bib NeuroFuzzy.sty pictures

# Which compilation model shall be used?
# Possible options:
#   latex    - tradirional TEX->DVI->PS model,
#   xelatex  - novaday TEX->PDF model using EPS pics.
#   pdflatex - novaday TEX->PDF model using all pic formats except EPS.

LATEX_MODEL=pdflatex

# Wich compilers shall be used?
pdflatex=pdflatex # may be pdflatex, lualatex etc.
xelatex=xelatex

#################################################

build=build

all: $(name).pdf

$(name).pdf: $(build)/$(main).pdf
	@echo; echo ===== CP; echo;
	@cp $< $@

ifeq ($(LATEX_MODEL), xelatex)
compiler=$(xelatex)
else
compiler=$(pdflatex)
endif

build:
	@mkdir $(build);
	@cd $(build) && ln -s $(FILES:%=../%) .

latex:
	@echo; echo ===== LaTeX; echo;
	@cd $(build); $(compiler) -shell-escape $(main).tex;

biber:
	@if test -f $(build)/$(main).bcf;\
	then\
		echo; echo ===== Biber; echo;\
		cd $(build) && biber $(main);\
	fi;

warnings:
	@echo; echo ===== WARNINGS; echo;
	@echo "---- Unused and unlabelled:"
	@cat $(build)/$(main).log | grep 'Package refcheck Warning' || echo "NONE"
	@echo "---- Unknown labels:"
	@cat $(build)/$(main).log | grep 'LaTeX Warning' | grep -v 'float specifier changed' || echo "NONE"

quick:
	@$(MAKE) latex
	@cp $(build)/$(main).pdf $(name).pdf

$(build)/$(main).pdf: $(FILES) Makefile build
	@$(MAKE) latex
	@$(MAKE) biber
	@$(MAKE) latex
	@$(MAKE) latex
	@$(MAKE) warnings

booklet.pdf: $(build)/$(main).log $(name).pdf
	@awk -f src/scripts/prepare_booklet_tex.awk < $(build)/$(main).log
	@sed "s/+++PDF+++/$(name).pdf/" < /tmp/booklet.tex > $(build)/booklet.tex
	@cd $(build) && pdflatex booklet.tex;
	@if test -f $(build)/booklet.pdf;\
		then mv $(build)/booklet.pdf .;\
	fi;

clean:
	@echo; echo ===== CLEAN; echo;
	@rm -f -r $(build)
	@rm -f ./*~
	@$(RM) -f `find . -name \*'-eps-converted-to.pdf'`

clobber: clean
	@echo; echo ===== CLOBBER; echo;
	@rm -f $(name).pdf
	@rm -f booklet.pdf

