OCAMLC = ocamlfind ocamlc
OCAMLOPT = ocamlfind ocamlopt
OCAMLFLAGS = -annot -g

PACKS = bitstring

.PHONY: all clean
all: fat.opt

fat.opt: fat_utils.cmx fat.cmx fat_shell.cmx
	$(OCAMLOPT) -linkpkg -package $(PACKS) -o $@ fat_utils.cmx fat.cmx fat_shell.cmx

%.cmx: %.ml
	$(OCAMLOPT) $(OCAMLFLAGS) -package $(PACKS),bitstring.syntax -syntax camlp4o -c -o $@ $<

%_gen: %.ml
	camlp4o $(shell ocamlfind query bitstring.syntax -r -format "-I %d %a" -predicates syntax,preprocessor) $< -printer o > $@.ml
	$(OCAMLOPT) $(OCAMLFLAGS) -package $(PACKS) -c -o $@ $@.ml

clean:
	rm -f *.cmx *.cmi *.cmo *.cmxa *.o $(EXECS)
