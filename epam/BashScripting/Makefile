TARGET = 01-bash_intro.pdf
TARGET += 02-bash_syntax.pdf
TARGET += 03-bash_syntax.pdf
TARGET += 04-bash_syntax.pdf
TARGET += 05-bash_advanced.pdf
TARGET += 06-bash_advanced.pdf

LATEXML=latexml
LATEXML_PARAMS=--inputencoding=utf8 --preload=beamer.cls --preload=t2aenc.def --nocomments
XMLWF=xmlwf
XMLWF_PARAMS=

LATEXML2OPENXML=java -jar latexml2openxml-0.0.1-SNAPSHOT-jar-with-dependencies.jar

.PHONY: all xml pptx tex clean

%.dvi: %.tex
	latex $<
	latex $<
	latex $<

%.ps: %.dvi
	dvips -j0 -Ppdf -o $@ $<

%.pdf: %.tex
	pdflatex -interaction=nonstopmode $<

%.xml: %.tex
	$(LATEXML) $(LATEXML_PARAMS) --destination=$@ $< &> $@.log
	$(XMLWF) $(XMLWF_PARAMS) $@

%.pptx: %.xml
	$(LATEXML2OPENXML) --slideshow=$@ $< &> $@.log

tex: $(TARGET)

xml: $(TARGET_XML)

pptx: $(TARGET_PPTX)

bib: programm.aux
	bibtex8 -s programm.aux

all: tex

clean: 
	@rm -f *.aux
	@rm -f *.vrb
	@rm -f *.snm
	@rm -f *.log
	@rm -f *.out
	@rm -f *.toc
	@rm -f *.nav
	@rm -f $(TARGET_PPTX)
	@rm -f $(TARGET_XML)
	@rm -f $(TARGET)
