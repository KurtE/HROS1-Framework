###############################################################
#
# Purpose: Makefile for "demo"
# Author.: robotis
# Version: 0.1
# License: GPL
#
###############################################################

TARGET = demo

#~~~~~~~~~~~~~~~~~~~~ Source Files ~~~~~~~~~~~~~~~~~~~~
SOURCES = \
		StatusCheck.cpp \
		main.cpp
		
OBJECTS:= $(notdir $(subst .cpp,.o,$(SOURCES)))

DEPS:= $(notdir $(subst .cpp,.d,$(SOURCES)))
		
#~~~~~~~~~~~~~~~~~~~~ Include Directories ~~~~~~~~~~~~~~~~~~~~
INCLUDE_DIRS = -I../../include -I../../../Framework/include

#~~~~~~~~~~~~~~~~~~~~ Library Directories ~~~~~~~~~~~~~~~~~~~~
LIBRARY_DIRS = -L../../lib/

#~~~~~~~~~~~~~~~~~~~~ Compiler Options ~~~~~~~~~~~~~~~~~~~~
CXX = g++
CXXFLAGS += -g -O2 -DLINUX -Wall $(INCLUDE_DIRS)
#CXXFLAGS += -O2 -DDEBUG -DLINUX -Wall $(INCLUDE_DIRS)


#~~~~~~~~~~~~~~~~~~~~ Linker Options ~~~~~~~~~~~~~~~~~~~~
LFLAGS += -g $(LIBRARY_DIRS) -lpthread -ljpeg -lrt -lbluetooth

OBJECTS = StatusCheck.o main.o


#~~~~~~~~~~~~~~~~~~~~ all ~~~~~~~~~~~~~~~~~~~~
all:  darwin.a begin gccversion build end

#~~~~~~~~~~~~~~~~~~~~ darwin.a ~~~~~~~~~~~~~~~~~~~~
darwin.a:
	cd ../../build; $(MAKE)

#~~~~~~~~~~~~~~~~~~~~ build ~~~~~~~~~~~~~~~~~~~~
build: $(TARGET)

%.o: ../src/%.cpp
	$(CXX) $(CXXFLAGS) -c $<

# added specific dependence on my own library...
$(TARGET): $(OBJECTS) ../../lib/darwin.a
	$(CXX) $(CFLAGS) $(OBJECTS) ../../lib/darwin.a -o $(TARGET) $(LFLAGS)
	chmod 755 $(TARGET)

MSG_BEGIN = -------- begin --------
MSG_END = --------  end  --------

#~~~~~~~~~~~~~~~~~~~~ Eye candy ~~~~~~~~~~~~~~~~~~~~
begin:
	@echo
	@echo $(MSG_BEGIN)

end:
	@echo $(MSG_END)
	@echo

gccversion:
	@$(CC) --version

#~~~~~~~~~~~~~~~~~~~~ clean ~~~~~~~~~~~~~~~~~~~~
clean: begin clean_list end

clean_list:
	-rm -f $(TARGET)
	-rm -f $(OBJECTS)
	-rm -f $(DEPS)
	-cd ../../build; make clean

#~~~~~~~~~~~~~~~~~~~~ tgz ~~~~~~~~~~~~~~~~~~~~
# useful to make a backup "make tgz"
tgz: clean
	mkdir -p backups
	tar czvf ./backups/DARwIn_demo_`date +"%Y_%m_%d_%H.%M.%S"`.tgz --exclude backups *

#~~~~~~~~~~~~~~~~~~~~ Dependency Generation
include $(notdir $(subst .cpp,.d,$(SOURCES)))

%.d: %.cpp
	$(CC) -M $(CXXFLAGS) $< > $@.$$$$; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@;  \
	rm -f $@.$$$$
