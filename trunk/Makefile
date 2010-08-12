pages=16
docs=1 2 3 4 5 6 7 8 9 16
pdfa=$(patsubst %,%-a.tmp,$(docs))
pdfb=$(patsubst %,%-b.tmp,$(docs))
pdfc=$(patsubst %,%-c.tmp,$(docs))

all:x.pdf

x.pdf:$(pdfa) $(pdfb) $(pdfc)
	gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOUTPUTFILE=x *.tmp
	mv x x.pdf

$(pdfa):%-a.tmp:%.ps
	./ps-crop $< 67 533 286 697 >$@.ps && ps2pdf $@.ps $@

$(pdfb):%-b.tmp:%.ps
	./ps-crop $< 67 314 286 478 >$@.ps && ps2pdf $@.ps $@

$(pdfc):%-c.tmp:%.ps
	./ps-crop $< 67 314 286 478 >$@.ps && ps2pdf $@.ps $@

$(patsubst %,%.ps,$(docs)):%.ps:a.ps
	psselect -p$(patsubst %.ps,%,$@) $< $@

a.ps:a.pdf
	pdf2ps a.pdf

clean:
	rm -f *.ps *-a *-b *-c *-a.pdf *-b.pdf *-c.pdf *.tmp
