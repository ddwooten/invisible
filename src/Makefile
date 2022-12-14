###############################################################################

# GNU Compiler:

CC  	 = g++
CCM      = g++
CFLAGS   = -Wall -ansi -ffast-math -O3 -std=c++17
LDFLAGS  = -lm -std=c++17

# Parallel calculation using Open MP:

CFLAGS  += -fopenmp
LDFLAGS += -fopenmp

# This is needed in newer gcc versions to supress some unnecessary warnings

#CFLAGS += -Wno-unused-but-set-variable

# Remove this if compilation with mpicc produces unnecessary warnings

#CFLAGS += -pedantic

# This is needed by new version of XCode in OS/X

#CFLAGS  += -D_FORTIFY_SOURCE=0

###############################################################################

# Intel Compiler:

#CC  	 = icc

# Optimization for Intel CPU's:

#CFLAGS   = -Wall -ansi -pedantic -xHost -ipo -DINTELCC

# Alternative:

#CFLAGS   = -Wall -ansi -pedantic -O3 -DINTELCC

#LDFLAGS  = -lm

# Parallel calculation using Open MP:

#CFLAGS  += -DOPEN_MP
#CFLAGS  += -openmp
#LDFLAGS += -openmp

###############################################################################

# Parallel calculation using MPI:

# NOTE: The use of hybrid MPI/OpenMP mode requires thread-safe MPI
#       implementation. Some MPI implementations, such as some versions (?) of
#       Open MPI are not thread safe, which will cause problems in memory 
#       management routines (calloc, realloc and free). These problems may
#       result in failure in memory allocation or unexpected behaviour due to
#       corrupted registers (?).

#CC  	 = mpicc
#CCM	 = mpicc
###############################################################################

# Debugging:

CFLAGS :=$(filter-out -O3,$(CFLAGS))
CFLAGS :=$(filter-out -ffast-math,$(CFLAGS))
CFLAGS  += -g -O0
LDFLAGS += -g

# Profiler:

#CFLAGS   += -p 
#LDFLAGS  += -p

###############################################################################

OBJS	=	main.o \
		example.o 

###############################################################################

EXE     = Invisible

DATE 	= -DMC_COMPILE_DATE="\"`date `\""

# Get number of bits:

shell = $SHELL
lbits := $(shell getconf LONG_BIT)

# Use this to override the 64 bit check

#lbits = 64

###############################################################################
all:    $(EXE)
	@echo "Invisible Compiled OK."

$(EXE): $(OBJS) 
	$(CCM) $(OBJS) $(LDFLAGS) -o $(EXE)

clean:	
	$(RM) $(OBJS) $(FOBJS) $(OBSOLETE)

###############################################################################

main.o: main.cpp 
	$(CC) $(CFLAGS) -c main.cpp

example.o: example.cpp example.h
	$(CC) $(CFLAGS) -c example.cpp 
