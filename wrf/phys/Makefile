# Makefile 
#
.SUFFIXES:
.SUFFIXES: .o .F

include ../../hrldas/user_build_options

OBJS = \
	module_sf_noahmpdrv.o \
	module_sf_noahmplsm.o \
	module_sf_noahmp_glacier.o \
	module_sf_noahmp_groundwater.o \
	module_sf_gecros.o \
	module_sf_urban.o \
	module_sf_bep.o \
	module_sf_bem.o \
	module_sf_bep_bem.o

CPPHRLDAS = -D_HRLDAS_OFFLINE_

all:	$(OBJS)

.F.o:
	@echo ""
	$(RM) $(*).f90
	$(CPP) $(CPPFLAGS) $(CPPHRLDAS) $(*).F > $(*).f90
	$(COMPILERF90) -o $(@) -c -I../../hrldas/Utility_routines $(F90FLAGS) $(FREESOURCE) $(*).f90
	@echo ""

#
# Dependencies:
#
module_sf_noahmplsm.o:	module_sf_gecros.o
module_sf_noahmpdrv.o:	module_sf_noahmplsm.o module_sf_noahmp_glacier.o module_sf_noahmp_groundwater.o \
                        module_sf_urban.o module_sf_bep.o module_sf_bep_bem.o
module_sf_noahmp_groundwater.o: module_sf_noahmplsm.o
module_sf_bep.o:	module_sf_urban.o
module_sf_bep_bem.o:	module_sf_urban.o module_sf_bem.o

#
# This command cleans up object (etc) files:
#

clean:
	$(RM) *.o *.mod *.stb *~ *.f90

