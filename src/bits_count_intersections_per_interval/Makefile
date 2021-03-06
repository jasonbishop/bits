include ../../defs.local
UTILITIES_DIR = ../utils/
OBJ_DIR = ../../obj/
BIN_DIR = ../../bin/

# -------------------
# define our includes
# -------------------
INCLUDES = -I$(UTILITIES_DIR)/bedFile/ \
           -I$(UTILITIES_DIR)/version/ \
           -I$(UTILITIES_DIR)/gzstream/ \
           -I$(UTILITIES_DIR)/genomeFile/ \
           -I$(UTILITIES_DIR)/lineFileUtilities/ \
           -I$(UTILITIES_DIR)/fileType/ \
           -I$(UTILITIES_DIR)/bits/interval_intersection/lib/seq \
		   -I$(UTILITIES_DIR)/bits/utils/c/mt/ \
		   -I$(UTILITIES_DIR)/bits/utils/c/file_read/ \
		   -I$(UTILITIES_DIR)/bits/utils/c/timer/
# ----------------------------------
# define our source and object files
# ----------------------------------
SOURCES= bits_count_per_interval_main.cpp \
		 bits_count_per_interval.cpp 
OBJECTS= $(SOURCES:.cpp=.o)
_EXT_OBJECTS=bedFile.o \
			 lineFileUtilities.o \
			 gzstream.o \
			 fileType.o \
			 interval.o \
			 bsearch.o \
			 mt.o \
			 timer.o \
			 file_read.o \
			 genomeFile.o
EXT_OBJECTS=$(patsubst %,$(OBJ_DIR)/%,$(_EXT_OBJECTS))
BUILT_OBJECTS= $(patsubst %,$(OBJ_DIR)/%,$(OBJECTS))
PROGRAM= bits_count_per_interval

all: $(PROGRAM)

.PHONY: all

$(PROGRAM): $(BUILT_OBJECTS) $(EXT_OBJECTS)
	@echo " * linking $(PROGRAM)"
	$(CXX) $(LDFLAGS) $(CXXFLAGS) -o $(BIN_DIR)/$@ $^ $(LIBS) \
		$(LOCAL_LIBS) -lz -lgsl -lgslcblas -lm

$(BUILT_OBJECTS): $(SOURCES)
	@echo " * compiling" $(*F).cpp
	@$(CXX) -c -o $@ $(*F).cpp $(LDFLAGS) $(CXXFLAGS) $(INCLUDES) \
		$(LOCAL_INCLUDES)

$(EXT_OBJECTS):
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/lineFileUtilities/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bedFile/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/gzstream/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/genomeFile/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/fileType/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bits/interval_intersection/lib/seq
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bits/binary_search/lib/seq
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bits/utils/c/mt/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bits/utils/c/timer/
	@$(MAKE) --no-print-directory -C $(UTILITIES_DIR)/bits/utils/c/file_read/

clean:
	@echo "Cleaning up."
	@rm -f $(OBJ_DIR)/* $(BIN_DIR)/*

.PHONY: clean
