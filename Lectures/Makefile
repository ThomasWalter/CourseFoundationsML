# Makefile for the "Fondamentaux du ML" slides
# Requires latexmk >= 4.70 (for -usepretex)
#
#   make            -> full deck + one PDF per chapter
#   make full       -> full deck only
#   make chapters   -> all chapter PDFs
#   make erm        -> one chapter (pdf/erm.pdf)
#   make -j4        -> build in parallel (separate job names, no conflicts)
#   make clean / make distclean

MASTER   := FoundationsML_complete
CHAPTERS := intro erm modelsel trees dimred
OUTDIR   := pdf
LATEXMK  := latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=$(OUTDIR)

CHAPTER_PDFS := $(addprefix $(OUTDIR)/,$(addsuffix .pdf,$(CHAPTERS)))

.PHONY: all full chapters clean distclean FORCE $(CHAPTERS)

all: full chapters

full: $(OUTDIR)/$(MASTER).pdf

chapters: $(CHAPTER_PDFS)

# latexmk tracks dependencies (chapters, figures...) itself, so always call it
$(OUTDIR)/$(MASTER).pdf: FORCE
	$(LATEXMK) $(MASTER).tex

$(OUTDIR)/%.pdf: FORCE
	$(LATEXMK) -jobname=$* -usepretex='\def\selectedchapter{$*}' $(MASTER).tex

# Shortcuts: "make erm" builds pdf/erm.pdf
$(CHAPTERS): %: $(OUTDIR)/%.pdf

clean:
	cd $(OUTDIR) 2>/dev/null && rm -f *.aux *.log *.nav *.out *.snm *.toc *.vrb \
	  *.fls *.fdb_latexmk *.synctex.gz || true

distclean:
	rm -rf $(OUTDIR)

FORCE:
