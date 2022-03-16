SHELL := /bin/bash

MDIR=../../modules
BDIR=build
DDIR=doc

DOXYGEN := doxygen
MAINPAGE = juce_modules_mainpage.dox

SOURCE_FILES := $(shell find $(MDIR) -type f \
	-name "juce_*.h" -or -name "juce_*.dox" \
	-name "foleys_*.h" -or -name "foleys_*.dox" \
	| sed 's/ /\\ /g')

.PHONY: clean

co:
	make clean
	make $(DDIR)/index.html
	open $(DDIR)/index.html

$(DDIR)/index.html: $(BDIR)/juce_modules.dox Doxyfile
	/bin/cp $(MAINPAGE) $(BDIR)
	$(DOXYGEN)

$(BDIR)/juce_modules.dox: process_source_files.py $(SOURCE_FILES)
	python $< $(MDIR) $(BDIR)

# Seems to not include juce_* !?
#	echo SOURCE_FILES from $(MDIR) = $(SOURCE_FILES) > /dev/null

i install: $(DDIR)/index.html
	rsync -auv $(DDIR)/ ccrma-gate.stanford.edu:~jos/web/juce_modules

clean:
	rm -rf $(BDIR) $(DDIR)
