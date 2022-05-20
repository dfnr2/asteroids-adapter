NAME=asteroids-adapter
PROJECT_DESC="Asteroids PCB CABINET ADAPTER"
VARIANTNAME=Production
BOARDREV=2
BOARDREVMINOR=
SCHEMATIC_REV=0
PROJECT_REV=0
PCBREV=0$(BOARDREV)
SCHREV=$(BOARDREV).$(SCHEMATIC_REV)
PRJREV=$(BOARDREV).$(SCHEMATIC_REV).$(PROJECT_REV)
PCBNAME=$(NAME)-Rev_$(PCBREV)$(BOARDREVMINOR)
SCHNAME=$(NAME)-Rev_$(SCHREV)
PRJNAME=$(NAME)-Rev_$(PRJREV)$(BOARDREVMINOR)

PCBDIR="./PCB_dir"
PCBZIPFILE=$(PCBNAME)-pcbfab.zip
PKGZIPFILE=$(PRJNAME)-package.zip
BOMFILE=BOM-$(PRJNAME)-$(VARIANTNAME).csv

#README_STYLE=rst
README_STYLE=pdf

READMEFILEBASE=README-$(PRJNAME)
READMEFILETXT=$(READMEFILEBASE).rst
READMEFILEPDF=$(READMEFILEBASE).pdf
READMETARGET=readme$(README_STYLE)

RENDERFILE_TOP=Renderings-top-$(PRJNAME)-$(VARIANTNAME).jpg
RENDERFILE_BOTTOM=Renderings-bottom-$(PRJNAME)-$(VARIANTNAME).jpg
RENDERFILES=$(RENDERFILE_TOP) $(RENDERFILE_BOTTOM)
DUMMY_RENDERFILES=$(RENDERFILE_TOP)_ $(RENDERFILE_BOTTOM)_
GENERATED_SCHEMFILE=../$(NAME).pdf
STEPFILE=Model-3D-$(PCBNAME)-$(VARIANTNAME).step
DUMMY_STEPFILE="$(STEPFILE)_"
DUMMY_TARGETS=$(DUMMY_STEPFILE) $(DUMMY_RENDERFILES)
GENERATED_BOMFILE = ../$(NAME)_bom_$(PCBREV).csv



define README_TEXT
"$(NAME) \($(PROJECT_DESC)\)"\
|-----------------------------------------------------------------------------------|\
|This is the package for $(NAME) rev $(PRJREV).|\
|Service Requested\
|=================|\
|   * PCB and assembly to IPC class 3 standards\
|   * 0.62 inch FR4, 94V-0 marked\
|   * 2 layer stackup to be approved prior to manufacture\
|   * ENIG finish, RoHS compliant|\
|Standards\
|=========|\
|RoHS compliant\
||Programming and labeling of microcontroller\
|===========================================|\
|None\
||Testing\
|=======\
|   * Test 100% testing of assemblies\
|   * Standard PCB QA (bed of nails, test for shorts and opens)\
|\
||Tracking\
|========|\
|None\
|\
||Packaging\
|=========|\
|Standard Packaging\
||Production Package\
|==================|\
|The  ZIP file contains the following files:\
|   $(PCBZIPFILE)\
|+++A ZIP file containing Gerbers; drill file;\
|+++readme.txt\
|++++++readme file containing PCB fabrication directions; fab renderings, etc.\
|\
|$(READMEFILE)\
|+++This letter.\
|\
|$(RENDERFILE_TOP)\
|+++A JPEG file containing a reference for PCB parts placement, and 3D renderings of the front of the populated board (with components).\
|\
|$(RENDERFILE_BOTTOM)\
|+++A JPEG file containing a reference for PCB parts placement, and 3D renderings of the back of the populated board (with components).\
|\
|$(STEPFILE):\
|+++An exported 3D STEP file of the PCB with all components fitted.\
|\
|$(SCHEMFILE)\
|+++A PDF file containing the schematics for this PCB.\
|\
|$(BOMFILE)\
|+++BOM file, csv format\
|\
|Subdirectory: labels_dir\
|+++:$(PROJNAME)_labels.doc: Labels for final packaging.\
|\
|Subdirectory: programming_files_dir\
|+++empty, not applicable.\
|\
|Subdirectory containing programming files\
|+++empty, not applicable\
|\
|Subdirectory: diagrams_dir\
|+++empty\
|\
|Subdirectory containing diagrams or pictures related to production\
|+++empty\
|\
|Subdirectory: work_instructions_dir\
|+++Subdirectory containing work instructions, test procedures, etc.|\
|.. figure:: ./$(RENDERFILE_TOP)|\
|   TOP side rendering of populated PCB\
|.. figure:: ./$(RENDERFILE_BOTTOM)|\
|   TOP side rendering of populated PCB
endef


define RENDER_TOP_MSG
|The assembly rendering \"$(RENDERFILE_TOP)\"\
|must be manually generated with the following steps:\
|1) Bring up the 3D rendering from PCBNEW \(ALT-3\).  Select\
|the TOP view \(RightClick-"View Top"\).\
|2) Perform a screen capture.  Save the capture to the\
|production-package directory.  Select the dummy file name\
|"    \"$(RENDERFILE_TOP)_\""\
|and delete the trailing \"_\".  Then click Save.
endef

define RENDER_BOTTOM_MSG
|The assembly rendering \"$(RENDERFILE_BOTTOM)\"\
|must be manually generated with the following steps:\
|1) Bring up the 3D rendering from PCBNEW \(ALT-3\).  Select\
|the BOTTOM view \(RightClick-"View Bottom"\).\
|2) Perform a screen capture.  Save the capture to the\
|production-package directory.  Select the dummy file name\
|"    \"$(RENDERFILE_BOTTOM)_\""\
|and delete the trailing \"_\".  Then click Save.
endef

define BOM_MSG
|The BOM file must be manually generated.  The BOM file requires the KiBOM plugin.\
|Please ensure that KiBOM is installed.  To generate the BOM file:\
|1) Copy the file 'bom.ini' in the templates directory to the main directory:\
|\"   cp templates_dir/bom.ini ..\"\
|2) In EESChema, select Tools->Generate BOM.|\
|3) Select KIBOM_CLI and click \"Generate\"|
endef

define SCHEM_MSG
|The Schematic PDF file must be manually generated:\
|1) In EESChema, select File->Plot to bring up the Plot dialog\
|2) Select PDF output format.\
|3) Check "Plot Drawing Sheet"\
|4) Click "Plot All Pages"
endef

define STEPFILE_MSG
|The STEP file must be manually generated.\
|1) From PCBNEW, select File->Export->STEP\
|2) Save to the production package directory.  Select the placeholder filename:\
|"    $(STEPFILE)_"\
|3) Remove the trailing \"_\" and click "Save"
endef

# KiCad doesn't automate saving of rendering files, which must be
# screen-captured and saved as JPEG files. The STEP file must similarly be
# exported manually. the "dummies" target creates filename templates that can be
# selected and edited (by removing the trailing "_") to help ensure that the

all: dummies $(BOMFILE) $(RENDERFILES) $(SCHEMFILE) \
	$(READMETARGET) pkgzip

.phony: dummies
dummies:
	@echo "$(DUMMY_TARGETS)" | xargs -n 1 echo "+++ Creating placeholder: "
	@touch $(DUMMY_TARGETS)

.Phony: clean
clean:
	rm -fv  *.zip  $(DUMMY_TARGETS) *~ *_
	(cd PCB_dir; make clean)

.phony: veryclean
veryclean: clean
	rm -fv $(SCHEMFILE) $(RENDERFILES) $(BOMFILE)
	(cd PCB_dir; make veryclean)

$(BOMFILE):
	@if [ ! -f "$(GENERATED_BOMFILE)" ]; then \
		echo "$(BOM_MSG)"|tr '|' '\n';\
	else \
		echo "--> Found BOM: cp ../$(NAME)_bom_$(PCBREV).csv $(BOMFILE)";\
		cp ../$(NAME)_bom_$(PCBREV).csv $(BOMFILE);\
	fi

bomfile: $(BOMFILE)

$(SCHEMFILE):
	@if [ ! -f "$(GENERATED_SCHEMFILE)" ]; then \
		echo "$(SCHEM_MSG)"|tr '|' '\n'; \
	else \
		echo "--> Found Schematic PDF: $(GENERATED_SCHEMFILE)";\
		cp $(GENERATED_SCHEMFILE) $(SCHEMFILE);\
	fi

schemfile: $(SCHEMFILE)

.Phony: stepfile
stepfile:
	@if [ ! -f "$(STEPFILE)" ]; then\
		echo; \
		echo "$(STEPFILE_MSG)"|tr '|' '\n'; \
		echo; \
	else \
		echo "--> Found assembly STEP file: $(STEPFILE)"; \
	fi

.Phony: renderfiles
renderfiles: renderfile_top renderfile_bottom

.Phony: renderfile_top
renderfile_top:
	@if [ ! -f "$(RENDERFILE_TOP)" ]; then\
		echo; \
		echo "$(RENDER_BOTTOM_MSG)"|tr '|' '\n'; \
		echo; \
	else \
		echo "--> Found top assembly rendering: $(RENDERFILE_TOP)"; \
	fi

.Phony: renderfile_bottom
renderfile_bottom:
	@if [ ! -f "$(RENDERFILE_BOTTOM)" ]; then\
		echo; \
		echo "$(RENDER_TOP_MSG)"|tr '|' '\n'; \
		echo; \
	else \
		echo "--> Found bottom assembly rendering: $(RENDERFILE_BOTTOM)"; \
	fi

$(PCBZIPFILE):
	echo "Building PCB Zip file..."; (cd $(PCBDIR); make zip)

renderfiles: renderfile_top renderfile_bottom

readmetxt: $(READMEFILETXT)

readmepdf: $(READMEFILEPDF)

$(READMEFILETXT): Makefile
	@echo "Creating Readme File $(READMEFILETXT)."; \
	echo "$(README_TEXT)"|tr '|' '\n' | sed 's/+++/   /g'  > $(READMEFILETXT);

$(READMEFILEPDF): $(READMEFILETXT)
	@echo "Creating Readme File $(READMEFILEPDF)."; \
	pandoc -f rst -t pdf -o "$(READMEFILEPDF)" "$(READMEFILETXT)";


pkgzip: $(PCBZIPFILE) $(BOMFILE) $(RENDERFILES) $(READMEFILE)
	@echo removing old zip. . . \
	rm -rf $(PKGZIPFILE) \
	echo creating zip. . . \
	zip -9r $(PKGZIPFILE) \
	$(PCBZIPFILE) \
	$(READMEFILE) \
	$(SCHEMFILE) \
	$(RENDERFILES) \
	$(BOMFILE) \
	$(STEPFILE) \
	programming_files_dir \
	diagrams_dir \
	work_instructions_dir \
	labels_dir
