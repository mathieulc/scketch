.PHONY: all viewpdf pdf clean

TARGET       = mainos#diff#
SOURCE_FILES = $(TARGET).tex 
BIB_FILES    = $(wildcard vort_240419.bib)
FIGURES      = $(wildcard ../fig_os/*)

# Set the pdf reader according to the operating system
OS = $(shell uname)
ifeq ($(OS), Darwin)
	PDF_READER = open
endif
ifeq ($(OS), Linux)
	PDF_READER = evince
endif

all: pdf

viewpdf: pdf
	$(PDF_READER) $(TARGET).pdf &

pdf: $(TARGET).pdf

$(TARGET).pdf: $(SOURCE_FILES) $(BIB_FILES) $(FIGURES) copernicus.cls ../ametsoc2014.bst
	pdflatex $(TARGET).tex
	bibtex $(TARGET)
	pdflatex $(TARGET).tex # For biber
	pdflatex $(TARGET).tex

clean:
	rm -f $(TARGET).{ps,pdf,bcf,run.xml}
	for suffix in dvi aux bbl blg toc ind out brf ilg idx synctex.gz log; do \
		find . -name "*.$${suffix}" -delete; \
	done
