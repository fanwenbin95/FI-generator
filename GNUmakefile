FC = ifort
#-O0 -qopenmp 
# -check all  -check bounds  -check uninit -O0 -ftrapuv \
FFLAGS = -module mod -g  -traceback  -CB -debug all
LIB = -L${MKLROOT} -lmkl_rt
SRC = $(wildcard src/*)
OBJf90 = $(patsubst src/%.f90, %.o, $(filter %.f90, $(SRC)))
OBJmod = $(patsubst src/%.F90, %.m.o, $(filter %.F90, $(SRC)))
OBJcud = $(patsubst src/%.cu, %.cu.o, $(filter %.cu, $(SRC)))
EXE = bin/invariants

$(EXE): $(patsubst %.o, obj/%.o, $(OBJmod) $(OBJf90))
	$(FC) $(FFLAGS) $(LIB) \
	$+ -o $@
obj/%.o : src/%.f90
	$(FC) $(FFLAGS) -c $<  $(LIB) -o $@
obj/%.m.o : src/%.F90
	$(FC) $(FFLAGS) -c $<  $(LIB) -o $@
clean:
	rm -f obj/*.o mod/*.mod $(EXE)
