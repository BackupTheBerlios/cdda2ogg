# Makefile for CDDA2OGG
#

DESTDIR=
PREFIX=usr/local
DOCDIR=${PREFIX}/share/doc
PERL=/usr/bin/perl
VERSION=0.3.0

default	:	cdda2ogg.pl cdda2ogg.1 cdda2ogg.html cdda2ogg.ps

clean:
	-rm -f *.ps *.html *.1 *~~ cdda2ogg.pl

cdda2ogg.pl:	cdda2ogg.pl.in Makefile
	${PERL} -p -e 's/%%VERSION%%/${VERSION}/;'\
			cdda2ogg.pl.in > cdda2ogg.pl
	chmod 755 cdda2ogg.pl

cdda2ogg.1:	cdda2ogg.pl
	pod2man --center=" " cdda2ogg.pl > cdda2ogg.01
	${PERL} -p	-e 's/.if n .na/.\\\".if n .na/;'\
			cdda2ogg.01 > cdda2ogg.1
	rm cdda2ogg.01

cdda2ogg.html:	cdda2ogg.pl
	pod2html --infile=cdda2ogg.pl --outfile=cdda2ogg.html\
	--title "CDDA2OGG - Compact Disc Digital Audio to Ogg/Vorbis"

cdda2ogg.ps:	cdda2ogg.1
	groff -man -Tps cdda2ogg.1 > cdda2ogg.ps

install:	cdda2ogg.pl cdda2ogg.1 cdda2ogg.ps cdda2ogg.html
	install	-d	${DESTDIR}/${PREFIX}/bin\
				${DESTDIR}/${PREFIX}/share/cdda2ogg\
				${DESTDIR}/${PREFIX}/share/man/man1\
				${DESTDIR}/${DOCDIR}/cdda2ogg/
	install -m 755 	cdda2ogg.pl	${DESTDIR}/${PREFIX}/bin/cdda2ogg
	install -m 644 	cdda2ogg.1	${DESTDIR}/${PREFIX}/share/man/man1/cdda2ogg.1
	gzip						${DESTDIR}/${PREFIX}/share/man/man1/cdda2ogg.1
	install	-m 644	cdda2ogg.html ${DESTDIR}/${DOCDIR}/cdda2ogg/cdda2ogg.html
	install	-m 644	cdda2ogg.ps	${DESTDIR}/${DOCDIR}/cdda2ogg/cdda2ogg.ps

