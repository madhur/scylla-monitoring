# You can set these variables from the command line.
POETRY        = $(HOME)/.poetry/bin/poetry
SPHINXOPTS    =
SPHINXBUILD   = $(POETRY) run sphinx-build
PAPER         =
BUILDDIR      = _build
SOURCEDIR     = source

# Internal variables.
PAPEROPT_a4     = -D latex_paper_size=a4
PAPEROPT_letter = -D latex_paper_size=letter
ALLSPHINXOPTS   = -d $(BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) $(SPHINXOPTS) $(SOURCEDIR)

# the i18n builder cannot share the environment and doctrees with the others
I18NSPHINXOPTS  = $(PAPEROPT_$(PAPER)) $(SPHINXOPTS) $(SOURCEDIR)

.PHONY: all
all: dirhtml

.PHONY: pristine
pristine: clean
	git clean -dfX

.PHONY: setup
setup:
	./_utils/setup.sh

.PHONY: clean
clean:
	rm -rf $(BUILDDIR)/*

.PHONY: preview
preview: setup
	$(POETRY) run sphinx-autobuild -b dirhtml $(ALLSPHINXOPTS) $(BUILDDIR)/dirhtml --port 5500

.PHONY: dirhtml
dirhtml: setup
	$(SPHINXBUILD) -b dirhtml $(ALLSPHINXOPTS) $(BUILDDIR)/dirhtml
	@echo
	@echo "Build finished. The HTML pages are in $(BUILDDIR)/dirhtml."

.PHONY: singlehtml
singlehtml: setup
	$(SPHINXBUILD) -b singlehtml $(ALLSPHINXOPTS) $(BUILDDIR)/singlehtml
	@echo
	@echo "Build finished. The HTML page is in $(BUILDDIR)/singlehtml."

.PHONY: epub
epub: 	setup
	$(SPHINXBUILD) -b epub $(ALLSPHINXOPTS) $(BUILDDIR)/epub
	@echo
	@echo "Build finished. The epub file is in $(BUILDDIR)/epub."

.PHONY: epub3
epub3:	setup
	$(SPHINXBUILD) -b epub3 $(ALLSPHINXOPTS) $(BUILDDIR)/epub3
	@echo
	@echo "Build finished. The epub3 file is in $(BUILDDIR)/epub3."

.PHONY: dummy
dummy: 	setup
	$(SPHINXBUILD) -b dummy $(ALLSPHINXOPTS) $(BUILDDIR)/dummy
	@echo
	@echo "Build finished. Dummy builder generates no files."

.PHONY: linkcheck
linkcheck: setup
	$(SPHINXBUILD) -b linkcheck $(SOURCEDIR) $(BUILDDIR)/linkcheck

.PHONY: multiversion
multiversion: setup
	@mkdir -p $(HOME)/.cache/pypoetry/virtualenvs
	$(POETRY) run sphinx-multiversion $(SOURCEDIR) $(BUILDDIR)/dirhtml
	@echo
	@echo "Build finished. The HTML pages are in $(BUILDDIR)/dirhtml."

.PHONY: multiversionpreview
multiversionpreview: multiversion
	$(POETRY) run python3 -m http.server 5500 --directory $(BUILDDIR)/dirhtml

.PHONY: test
test: setup
	$(SPHINXBUILD) -b dirhtml $(TESTSPHINXOPTS) $(BUILDDIR)/dirhtml
	@echo
	@echo "Build finished. The HTML pages are in $(BUILDDIR)/dirhtml."

TESTSPHINXOPTS  = $(ALLSPHINXOPTS) -W --keep-going