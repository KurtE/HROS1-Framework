###############################################################
#
# Purpose: Makefile for "DARwIn Linux Framework"
# Author.: robotis
# Version: 0.1
# License: GPL
#
###############################################################

#~~~~~~~~~~~~~~~~~~~~ Output File Name ~~~~~~~~~~~~~~~~~~~~
TARGET = darwin.a

#~~~~~~~~~~~~~~~~~~~~ Include Directories ~~~~~~~~~~~~~~~~~~~~
CC = g++
AR = ar
ARFLAGS = cr

#~~~~~~~~~~~~~~~~~~~~ Include Directories ~~~~~~~~~~~~~~~~~~~~
INCLUDE_DIRS = -I. -I../include -I../../Framework/include 

#~~~~~~~~~~~~~~~~~~~~ Compiler Options ~~~~~~~~~~~~~~~~~~~~
CXXFLAGS += -fPIC -shared -O2 -DLINUX -D_GNU_SOURCE -Wall -g $(INCLUDE_DIRS) 
#CXXFLAGS += -O2 -DDEBUG -DLINUX -D_GNU_SOURCE -Wall -shared $(INCLUDE_DIRS)

#~~~~~~~~~~~~~~~~~~~~ Linker Options ~~~~~~~~~~~~~~~~~~~~
LFLAGS += -g -lpthread -ldl -lbluetooth -lncurses

#~~~~~~~~~~~~~~~~~~~~ Source Files ~~~~~~~~~~~~~~~~~~~~
SOURCES = \
		../../Framework/src/CM730.cpp     	\
		../../Framework/src/math/Matrix.cpp   \
		../../Framework/src/math/Plane.cpp    \
		../../Framework/src/math/Point.cpp    \
		../../Framework/src/math/Vector.cpp   \
		../../Framework/src/math/QuadraticStateTransform.cpp   \
		../../Framework/src/math/MotionState.cpp   \
		../../Framework/src/motion/JointData.cpp  	\
		../../Framework/src/motion/Kinematics.cpp 	\
		../../Framework/src/motion/MotionManager.cpp  \
		../../Framework/src/motion/MotionStatus.cpp   \
		../../Framework/src/motion/AngleEstimator.cpp \
		../../Framework/src/motion/modules/Action.cpp \
		../../Framework/src/motion/modules/Head.cpp   \
		../../Framework/src/motion/modules/Walking.cpp\
		../../Framework/src/vision/BallFollower.cpp   \
		../../Framework/src/vision/PS3BallFollower.cpp   \
		../../Framework/src/vision/LineFollower.cpp   \
		../../Framework/src/vision/RobotFollower.cpp   \
		../../Framework/src/vision/ConnectRegions.cpp   \
		../../Framework/src/vision/RadonTransform.cpp   \
		../../Framework/src/vision/BallTracker.cpp    \
		../../Framework/src/vision/ColorFinder.cpp    \
		../../Framework/src/vision/Image.cpp  		\
		../../Framework/src/vision/ImgProcess.cpp 	\
		../../Framework/src/controller/JoystickController.cpp \
		../../Framework/src/commander/SerialInputCommander.cpp	\
		../../Framework/src/minIni/minIni.cpp \
		streamer/httpd.cpp           \
		streamer/jpeg_utils.cpp      \
		streamer/mjpg_streamer.cpp   \
		LinuxActionScript.cpp   \
		LinuxCamera.cpp   \
		LinuxCM730.cpp    \
		LinuxMotionTimer.cpp    \
		LinuxNetwork.cpp

	   
#~~~~~~~~~~~~~~~~~~~~ Object Files ~~~~~~~~~~~~~~~~~~~~
OBJS:= $(subst .cpp,.o,$(SOURCES)) 


DEPS:= $(subst .cpp,.d,$(SOURCES))

#~~~~~~~~~~~~~~~~~~~~ all ~~~~~~~~~~~~~~~~~~~~
all: begin gccversion build end

#~~~~~~~~~~~~~~~~~~~~ build ~~~~~~~~~~~~~~~~~~~~
build: $(TARGET)

$(TARGET): $(OBJS)
	mkdir -p ../lib/
	$(AR) $(ARFLAGS) ../lib/$(TARGET) $(OBJS) 
#	$(CC) -o $(TARGET) $(OBJS) $(LFLAGS)

MSG_BEGIN = -------- begin --------
MSG_END = --------  end  --------

#~~~~~~~~~~~~~~~~~~~~ Eye candy ~~~~~~~~~~~~~~~~~~~~
begin:
	@echo
	@echo $(MSG_BEGIN)
	@echo ${OSTYPE}

end:
	@echo $(MSG_END)
	@echo

gccversion:
	@$(CC) --version


clean:
	-rm -f $(../lib/$(TARGET))
	-rm -f $(DEPS)
	-rm -f $(OBJS)

#~~~~~~~~~~~~~~~~~~~~ Dependency Generation
include $(subst .cpp,.d,$(SOURCES)) 

%.d: %.cpp
	$(CC) -M $(CXXFLAGS) $< > $@.$$$$; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@;  \
	rm -f $@.$$$$


