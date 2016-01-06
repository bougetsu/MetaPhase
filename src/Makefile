.KEEP_STATE:




# source code
# EXES: individual binary executables
# OBJS: non-executable object files
EXE = MetaPhase
OBJS = TextFileParsers.o LinkMatrix.o HierarchicalClustering.o TrueMapping.o ClusteringResult.o MetaAssembly.o MetaPhase.o

# compiler commands

CC      = g++
RM      = /bin/rm -rf
BACKUPS = *~ \\\#*\\\#


# compiler flags
CFLAGS = -Wall -g -O3
CFLAGS += -ansi
CFLAGS += -pedantic
#CFLAGS += -pg

# Directories for includes & linking flags
INCLUDE_DIR=include
INCLUDES=-I$(INCLUDE_DIR) -I$(METAPHASE_SAMTOOLS_DIR) -I$(METAPHASE_BOOST_DIR)

# Linking flags.  The environment variables BOOST_LIBS and SAMTOOLS_LIBS must be set or this won't work.
INC_LIBS=-L$(INCLUDE_DIR) -lJtime -lJgtools -lJmarkov
BOOST_LIBS=-L$(METAPHASE_BOOST_DIR)/stage/lib -lboost_filesystem -lboost_system #-lboost_regex
SAMTOOLS_LIBS=-L$(METAPHASE_SAMTOOLS_DIR) -lbam
LFLAGS = $(INC_LIBS) $(BOOST_LIBS) $(SAMTOOLS_LIBS) -lz -lpthread


# dependencies

.cc.o:  .cc
	$(CC) -c $< $(CFLAGS) $(INCLUDES)

all:    check-env libs $(EXE)

libs: check-env
	$(MAKE) -C include

MetaPhase:  check-env $(OBJS)
	$(CC) $(CFLAGS) $(OBJS) -o MetaPhase $(LFLAGS)

clean:
	$(RM) $(OBJS) core .make.state gmon.out
	#cd $(INCLUDE_DIR); make clean; cd -

clobber: clean
	$(RM) $(BACKUPS) $(EXE)

# Environment variable check.
check-env:
ifndef METAPHASE_SAMTOOLS_DIR
    $(error Environment variable $$METAPHASE_SAMTOOLS_DIR is undefined - please set to a directory containing the samtools package)
endif
ifndef METAPHASE_BOOST_DIR
    $(error Environment variable $$METAPHASE_BOOST_DIR is undefined - please set to a directory containing the root of the Boost package)
endif

