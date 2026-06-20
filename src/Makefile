OCAMLOPT = ocamlopt
OCAMLC = ocamlc
DIR = xmlerr
OCAMLDIR = $(shell $(OCAMLC) -where)
DESTDIR = $(OCAMLDIR)/$(DIR)
DOCDIR = /usr/local/share/doc
DESTDOC = $(DOCDIR)/$(DIR)

all: lib opt
lib: xmlerr.cma
opt: xmlerr.cmxa

# Build Xmlerr

xmlerr.cmi: xmlerr.mli
	$(OCAMLC) -c $<

xmlerr.cmo: xmlerr.ml xmlerr.cmi
	$(OCAMLC) -c $<

xmlerr.cmx: xmlerr.ml xmlerr.cmi
	$(OCAMLOPT) -c $<

xmlerr.cma: xmlerr.cmo
	$(OCAMLC) -a -o $@ $<

xmlerr.cmxa: xmlerr.cmx
	$(OCAMLOPT) -a -o $@ $<

INSTALL_DIR = install -d -m 755
INSTALL_FILE = install -m 644

RMDIR = rmdir
MKDIR = mkdir -p

install: xmlerr.cmi
	$(INSTALL_DIR) $(DESTDIR)
	$(INSTALL_DIR) $(DESTDOC)
	$(INSTALL_FILE) xmlerr.mli $(DESTDIR)/
	$(INSTALL_FILE) xmlerr.cmi $(DESTDIR)/
	test -f xmlerr.cmo  && $(INSTALL_FILE) xmlerr.cmo  $(DESTDIR)/ || :
	test -f xmlerr.cma  && $(INSTALL_FILE) xmlerr.cma  $(DESTDIR)/ || :
	test -f xmlerr.cmx  && $(INSTALL_FILE) xmlerr.cmx  $(DESTDIR)/ || :
	test -f xmlerr.cmxa && $(INSTALL_FILE) xmlerr.cmxa $(DESTDIR)/ || :
	$(INSTALL_FILE) ../README $(DESTDOC)/

uninstall:
	$(RM) $(DESTDIR)/*
	$(RM) $(DESTDOC)/*
	$(RMDIR) $(DESTDIR)
	$(RMDIR) $(DESTDOC)

OCAMLDOC = ocamldoc

doc:
	$(MKDIR) doc
	$(OCAMLDOC) -html -d doc \
	  xmlerr.mli \
	  #End

clean:
	$(RM) *.[oa] *.so *.dll *.cm[ioax] *.cmx[as] *.exe *.opt *.byte

