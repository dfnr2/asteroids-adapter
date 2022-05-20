PROJECT_DESC="Asteroids PCB to Cabinet Adapter"
BARENAME=asteroids-adapter
REV=2
BASENAME=$(BARENAME)-Rev_$(REV)
VARIANT=
NAME=$(BASENAME)$(VARIANT)

#README_STYLE=rst
README_STYLE=pdf

READMEFILEBASE=README-PCB-$(NAME)
READMEFILETXT=$(READMEFILEBASE).rst
READMEFILEPDF=$(READMEFILEBASE).pdf
READMETARGET=readme$(README_STYLE)

TOP_SOLDER_EXT = gts
TOP_SOLDER_DSC = F_Mask
TOP_SOLDER_GBR = "$(BASENAME)_$(TOP_SOLDER_DSC).$(TOP_SOLDER_EXT)"
TOP_COPPER_EXT = gtl
TOP_COPPER_DSC = F_Cu
TOP_COPPER_GBR = "$(BASENAME)_$(TOP_COPPER_DSC).$(TOP_COPPER_EXT)"
TOP_SILK_EXT = gto
TOP_SILK_DSC = F_Silkscreen
TOP_SILK_GBR = "$(BASENAME)_$(TOP_SILK_DSC).$(TOP_SILK_EXT)"
BOT_SOLDER_EXT = gbs
BOT_SOLDER_DSC = B_Mask
BOT_SOLDER_GBR = "$(BASENAME)_$(BOT_SOLDER_DSC).$(BOT_SOLDER_EXT)"
BOT_COPPER_EXT = gbl
BOT_COPPER_DSC = B_Cu
BOT_COPPER_GBR = "$(BASENAME)_$(BOT_COPPER_DSC).$(BOT_COPPER_EXT)"
BOT_SILK_EXT = gbo
BOT_SILK_DSC = B_Silkscreen
BOT_SILK_GBR = "$(BASENAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT)"
OUTLN_EXT = gm1
OUTLN_DSC = Edge_Cuts
OUTLN_GBR = "$(BASENAME)_$(OUTLN_DSC).$(OUTLN_EXT)"
DRILL_EXT = DRL

TOP_PASTE_EXT = gtp
TOP_PASTE_DSC = F_Paste
TOP_PASTE_GBR = "$(BASENAME)_$(TOP_PASTE_DSC).$(TOP_PASTE_EXT)"
BOT_PASTE_EXT = gbp
BOT_PASTE_DSC = B_Paste
BOT_PASTE_GBR = "$(BASENAME)_$(BOT_PASTE_DSC).$(BOT_PASTE_EXT)"

GND1_EXT = g2
GND1_DSC = In1_Cu
GND1_GBR = "$(BASENAME)_$(GND1_DSC).$(GND1_EXT)"
GND2_EXT = g3
GND2_DSC = In2_Cu
GND2_GBR = "$(BASENAME)_$(GND2_DSC).$(GND2_EXT)"

OUTPUT_EXTS = $(addprefix *., $(TOP_SOLDER_EXT) $(TOP_COPPER_EXT) $(TOP_SILK_EXT) \
               $(BOT_SOLDER_EXT) $(BOT_COPPER_EXT) $(BOT_SILK_EXT) \
			   $(OUTLN_EXT) $(DRILL_EXT)) \
			   $(TOP_PASTE_EXT) $(BOT_PASTE_EXT)
#			   $(GND1_EXT) $(GND2_EXT)

DRILDIR = outputs
GERBDIR = outputs
FAB_TOP = $(NAME)-render-top-view.jpg
FAB_BOTTOM = $(NAME)-render-bottom-view.jpg
FAB_FILES = $(FAB_TOP) $(FAB_BOTTOM)
FAB_DUMMIES = $(FAB_TOP)_ $(FAB_BOTTOM)_

DUMMY_TARGETS = $(FAB_DUMMIES)

ZIPFILE = ../$(NAME)-pcbfab.zip

define FAB_TOP_MSG
|The assembly rendering \"$(FAB_TOP)\"\
|must be manually generated with the following steps:|\
|1) Bring up the 3D rendering from PCBNEW \(ALT-3\).|\
|2) Deselect the 3D model visibility for all components.|\
|3) Select the TOP view \(RightClick-"View Top"\).|\
|2) Perform a screen capture.  Save the capture to the\
|\"production-package/PCB_dir\" directory.  Select the dummy file name|\
|"    \"$(FAB_TOP)_\""|\
|and delete the trailing \"_\".  Then click Save.
endef

define FAB_BOTTOM_MSG
|The assembly rendering \"$(FAB_BOTTOM)\"\
|must be manually generated with the following steps:|\
|1) Bring up the 3D rendering from PCBNEW \(ALT-3\).|\
|2) Deselect the 3D model visibility for all components.|\
|3) Select the BOTTOM view \(RightClick-"View Bottom"\).|\
|2) Perform a screen capture.  Save the capture to the\
|\"production-package/PCB_dir\" directory.  Select the dummy file name|\
|"    \"$(FAB_BOTTOM)_\""|\
|and delete the trailing \"_\".  Then click Save.
endef

define README_TEXT
"$(BARENAME)  \($(PROJECT_DESC)\)"\
|------------------------------------------------------------------------------------|\
||:Board: "$(BASENAME)"\
||Service\
|=======|\
|   * Manufacturing and inspection to IPC class 3 standard.\
|   * RoHS compliant\
|   * PCB Material: FR4\
|   * 94V-0 marking\
|   * Layers: 2\
|   * Copper thickness: 1 oz all layers\
|   * Finish: ENIG|\
|   * Stackup: All tolerancec 10%\
|       1. Total thickness: 0.062\"\
|       1. top layer    1oz copper\
|       1. core         0.059\"\
|       1. bottom layer 1oz copper\
|\
|Files\
|=====|\
|:BOARD OUTLINE: - :code:\`"$(OUTLN_GBR)"\`\
|:TOP LAYER: - :code:\`"$(TOP_COPPER_GBR)"\`\
|:BOTTOM LAYER: - :code:\`"$(BOT_COPPER_GBR)"\`\
|:TOP SOLDER MASK: - :code:\`"$(TOP_SOLDER_GBR)"\`\
|:BOTTOM SOLDER MASK: - :code:\`"$(BOT_SOLDER_GBR)"\`\
|:TOP SILK SCREEN: - :code:\`"$(TOP_SILK_GBR)"\`\
|:BOTTOM SILK SCREEN: - :code:\`"$(BOT_SILK_GBR)"\`\
|:EXCELLON DRILL (Plated): - :code:\`"$(BASENAME)-PTH.DRL"\`\
|:EXCELLON DRILL (Non-plated): :code:\`"$(BASENAME)-NPTH.DRL"\`\
||Fab Drawings\
|============|\
|:$(FAB_TOP): - :code:\`3D rendering of the top of the bare PCB\`\
|:$(FAB_BOTTOM): - :code:\`3D rendering of the bottom of the bare PCB\`\
|\
|.. figure:: ./$(FAB_TOP)||\
|   TOP side rendering of bare PCB||\
|.. figure:: ./$(FAB_BOTTOM)||\
|   BOTTOM side rendering of bare PCB||\
|General Info\
|============|\
|   * This board was developed with Kicad 6\
|   * The Gerber files are in 2.5 RS274X format.\
||Special Instructions\
|====================|\
|  * Please note there are TWO Excellon Drill files, one for plated through holes (PTH), and one for non-plated through holes (NPTH).\
|  * The board outline is delineated in the Gerber file "$(OUTLN_GBR)"|\
|Thanks.
endef

define DRL_FAIL
|Missing drill file.  To generate the drill files, within PCBNew:|\
|- Select File->Plot.  Click "Generate Drill Files" at the bottom right side of the dialog.\
|- Select the following options:\
|  * Excellon, \"Use route command\"\
|  * Drill origin: Absolute\
|  * Drill units: inches\
|  * Zeros Format: Decimal format\
|  * Precision: 2.4\
|- Select \"Generate Drill File\"|
endef

define GBR_FAIL
|Missing gerber file.  To generate the gerber files, within PCBNew:|\
|- Select File->Plot.  Click "Generate Drill Files" at the bottom right side of the dialog.\
|- Select the following layers:\
|  * F.Cu\
|  * B.Cu\
|  * F.Silkscreen\
|  * B.Silkscreen\
|  * F.Paste\
|  * B.Paste\
|  * F.Mask\
|  * B.Mask\
|  * Edge.Cuts|
endef


all: dummies copy renderfiles $(READMETARGET)

readmetxt: $(READMEFILETXT)

readmepdf: $(READMEFILEPDF)

$(READMEFILETXT): Makefile
	@echo "Creating Readme File $(READMEFILETXT)."; \
	echo "$(README_TEXT)"|tr '|' '\n' | sed 's/+++/   /g'  > $(READMEFILETXT);

$(READMEFILEPDF): $(READMEFILETXT)
	@echo "Creating Readme File $(READMEFILEPDF)."; \
	pandoc -f rst -t pdf -o "$(READMEFILEPDF)" "$(READMEFILETXT)";


.Phony: renderfiles
renderfiles: renderfile_top renderfile_bottom

.Phony: renderfile_top
renderfile_top:
	@if [ ! -f "$(FAB_TOP)" ]; then\
		echo; \
		echo "$(FAB_TOP_MSG)"|tr '|' '\n'; \
		echo; \
	else \
		echo "--> Found top assembly rendering: $(FAB_TOP)"; \
	fi

.Phony: renderfile_bottom
renderfile_bottom:
	@if [ ! -f "$(FAB_BOTTOM)" ]; then\
		echo; \
		echo "$(FAB_TOP_MSG)"|tr '|' '\n'; \
		echo; \
	else \
		echo "--> Found bottom assembly rendering: $(FAB_BOTTOM)"; \
	fi

renderfiles: renderfile_top renderfile_bottom

clean:
	rm -f $(OUTPUT_EXTS) $(READMEFILETXT) $(READMEFILEPDF) *.zip $(DUMMY_TARGETS) *_

veryclean:
	rm -rfv outputs $(NAME)* $(BARENAME)*
	rm -rfv *.jpg *.JPG *.pdf *.pdf *.png *.PNG

.PHONY: dummies
dummies:
	@echo "Making placeholder filenames:"
	@echo "$(DUMMY_TARGETS)" | xargs -n 1 echo +++
	@touch $(DUMMY_TARGETS)


gvp: gvp_template.gvp
	sed -e "s/@@NAME@@/$(NAME)/" < $< > $(NAME).gvp

copy:
	cp $(DRILDIR)/$(BARENAME)-PTH.$(DRILL_EXT) ./$(NAME)-PTH.$(DRILL_EXT) || echo "$(DRILL_FAIL)"|tr '|' '\n'
	cp $(DRILDIR)/$(BARENAME)-NPTH.$(DRILL_EXT) ./$(NAME)-NPTH.$(DRILL_EXT) || echo "$(DRILL_FAIL)"|tr '|' '\n'
	cp $(GERBDIR)/$(BARENAME)-$(TOP_SOLDER_DSC).$(TOP_SOLDER_EXT) ./$(NAME)_$(TOP_SOLDER_DSC).$(TOP_SOLDER_EXT) || echo "$(GBR_FAIL)" | tr '|' '\n'
	cp $(GERBDIR)/$(BARENAME)-$(TOP_COPPER_DSC).$(TOP_COPPER_EXT) ./$(NAME)_$(TOP_COPPER_DSC).$(TOP_COPPER_EXT)
	cp $(GERBDIR)/$(BARENAME)-$(TOP_SILK_DSC).$(TOP_SILK_EXT) ./$(NAME)_$(TOP_SILK_DSC).$(TOP_SILK_EXT)
	cp $(GERBDIR)/$(BARENAME)-$(BOT_SILK_DSC).$(BOT_SILK_EXT) ./$(NAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT)
	cp $(GERBDIR)/$(BARENAME)-$(BOT_SOLDER_DSC).$(BOT_SOLDER_EXT) ./$(NAME)_$(BOT_SOLDER_DSC).$(BOT_SOLDER_EXT)
	cp $(GERBDIR)/$(BARENAME)-$(BOT_COPPER_DSC).$(BOT_COPPER_EXT) ./$(NAME)_$(BOT_COPPER_DSC).$(BOT_COPPER_EXT)
	cp $(GERBDIR)/$(BARENAME)-$(OUTLN_DSC).$(OUTLN_EXT) ./$(NAME)_$(OUTLN_DSC).$(OUTLN_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(GND1_DSC).$(GND1_EXT) ./$(NAME)_$(GND1_DSC).$(GND1_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(GND2_DSC).$(GND2_EXT) ./$(NAME)_$(GND2_DSC).$(GND2_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(TOP_PASTE_DSC).$(TOP_PASTE_EXT) ./$(NAME)_$(TOP_PASTE_DSC).$(TOP_PASTE_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(PWR1_DSC).$(PWR1_EXT) ./$(NAME)_$(PWR1_DSC).$(PWR1_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(PWR2_DSC).$(PWR2_EXT) ./$(NAME)_$(PWR2_DSC).$(PWR2_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(BOT_PASTE_DSC).$(BOT_PASTE_EXT) ./$(NAME)_$(BOT_PASTE_DSC).$(BOT_PASTE_EXT)
#	cp $(GERBDIR)/$(BARENAME)-$(BOT_SILK_DSC).$(BOT_SILK_EXT) ./$(NAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT)

gerbv:
	gerbv \
	$(NAME)_$(OUTLN_DSC).$(OUTLN_EXT) \
	$(NAME)-PTH.$(DRILL_EXT) \
	$(NAME)-NPTH.$(DRILL_EXT) \
	$(NAME)_$(TOP_SOLDER_DSC).$(TOP_SOLDER_EXT) \
	$(NAME)_$(TOP_COPPER_DSC).$(TOP_COPPER_EXT) \
	$(NAME)_$(TOP_PASTE_DSC).$(TOP_PASTE_EXT) \
	$(NAME)_$(TOP_SILK_DSC).$(TOP_SILK_EXT) \
	$(NAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT) \
	$(NAME)_$(BOT_SOLDER_DSC).$(BOT_SOLDER_EXT) \
	$(NAME)_$(BOT_COPPER_DSC).$(BOT_COPPER_EXT) \
	$(NAME)_$(GND1_DSC).$(GND1_EXT) \
	$(NAME)_$(GND2_DSC).$(GND2_EXT)
#	$(NAME)_$(BOT_PASTE_DSC).$(BOT_PASTE_EXT) \
#	$(NAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT) \
#	$(NAME)_$(PWR1_DSC).$(PWR1_EXT) \
#	$(NAME)_$(PWR2_DSC).$(PWR2_EXT) \

zip: all
	rm -f $(ZIPFILE)
	zip -9 $(ZIPFILE) \
	$(NAME)_$(OUTLN_DSC).$(OUTLN_EXT) \
	$(NAME)-PTH.$(DRILL_EXT) \
	$(NAME)-NPTH.$(DRILL_EXT) \
	$(NAME)_$(TOP_SOLDER_DSC).$(TOP_SOLDER_EXT) \
	$(NAME)_$(TOP_COPPER_DSC).$(TOP_COPPER_EXT) \
	$(NAME)_$(TOP_SILK_DSC).$(TOP_SILK_EXT) \
	$(NAME)_$(BOT_SOLDER_DSC).$(BOT_SOLDER_EXT) \
	$(NAME)_$(BOT_COPPER_DSC).$(BOT_COPPER_EXT) \
	$(FAB_FILES) \
	$(READMEFILE)
#	$(NAME)_$(GND1_DSC).$(GND1_EXT) \
#	$(NAME)_$(GND2_DSC).$(GND2_EXT) \
#	$(NAME)_$(TOP_PASTE_DSC).$(TOP_PASTE_EXT) \
#	$(NAME)_$(BOT_PASTE_DSC).$(BOT_PASTE_EXT) \
#	$(NAME)_$(BOT_SILK_DSC).$(BOT_SILK_EXT) \
#	$(NAME)_$(PWR1_DSC).$(PWR1_EXT) \
#	$(NAME)_$(PWR2_DSC).$(PWR2_EXT) \
