#================================================================================
#
# Makefile for JCSDA CRTM library build
#
# $Id: makefile 22707 2012-11-21 21:09:10Z paul.vandelst@noaa.gov $
#
#================================================================================

# Define macros
include make.macros


# Main targets
all $(LIBRARY):  libsrc/all

test: $(LIBRARY) install test/all


# Cleanup targets
clean: libsrc/clean test/clean

distclean: clean
	$(REMOVE) -r $(LIB_DIR)
	$(REMOVE) -r $(INC_DIR)


# Installation targets
install: install_lib install_inc

install_lib: $(LIB_DIR) $(LIBRARY)
	@echo; echo "Installing $(LIBRARY) in `pwd`/$(LIB_DIR)"; \
	$(COPY) $(LIBSRC_DIR)/$(LIBRARY) $(LIB_DIR); \
	echo
        
install_inc: $(INC_DIR) $(LIBRARY)
	@echo; echo "Installing *.$(EXT_MOD) in `pwd`/$(INC_DIR)"; \
	$(COPY) $(LIBSRC_DIR)/*.$(EXT_MOD) $(INC_DIR); \
	echo
        
# ...Create directories if necessary
$(LIB_DIR) \
$(INC_DIR) :
	- test -d $@ || mkdir $@


# Test results update target
update: test/update


# Subtargets
libsrc/all       \
libsrc/clean     \
test/all         \
test/clean       \
test/update      \
:
	@subdir=`echo $@ | sed 's,/.*,,'`; \
	target=`echo $@ | sed 's,.*/,,'`; \
	$(MAKE) -s SUBDIR=$$subdir TARGET=$$target subdir_target


subdir_target:
	@echo ""
	@cd $(SUBDIR) && \
	    echo "Making \`$(TARGET)' in directory `pwd`" && \
	    echo "" && \
	    $(MAKE) -s $(TARGET) || exit 1
	@echo ""
	@echo "Returning to directory `pwd`"
	@echo ""
