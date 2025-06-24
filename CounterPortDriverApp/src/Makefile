TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

#=============================
# Build the IOC application

USR_INCLUDES += -I$(BOOST_INCLUDE)
USR_INCLUDES += -I$(CPSW_FRAMEWORK_INCLUDE)
USR_INCLUDES += -I$(YAML_INCLUDE)
USR_INCLUDES += -I$(YAMLREADER_INCLUDE)
USR_INCLUDES += -I$(DEVICELIB_INCLUDE)
USR_INCLUDES += -I$(FFTW_INCLUDE)

#USR_INCLUDES 			  += -I$(EPICS_MODULES)/WaveformReaderAsyn/src
# LukasWaveformReader_DIR     = $(EPICS_MODULES)/WaveformReaderAsyn/lib/rhel9-x86_64
LukasWaveformReader_DIR     = $(WAVEFORMREADERASYN_LIB)

# adding this for testing
cpsw_DIR         = $(CPSW_FRAMEWORK_LIB)
yaml-cpp_DIR     = $(YAML_LIB)
deviceLib_DIR    = $(DEVICELIB_LIB)
yamlReader_DIR   = $(YAMLREADER_LIB)
fftw3_DIR		 = $(FFTW_LIB)
boost_system_DIR = $(BOOST_LIB)
tirpc_DIR         = $(TIRPC_LIB)
USR_LIBS_Linux += fftw3
USR_LIBS_Linux += LukasWaveformReader
USR_LIBS_Linux += cpsw
USR_LIBS_Linux += boost_system
USR_LIBS_Linux += yaml-cpp
USR_LIBS_Linux += yamlReader
USR_LIBS_Linux += deviceLib

ifeq ($(NEEDS_TIRPC),YES)
USR_LIBS_Linux += tirpc
endif

PROD_IOC = CounterPortDriver
# CounterPortDriver.dbd will be created and installed

# $(COMMON_DIR)/CounterPortDriver.dbd: $(COMMON_DIR)/waveform.dbd

DBD += CounterPortDriver.dbd

# CounterPortDriver.dbd will be made up from these files:
CounterPortDriver_DBD += base.dbd
CounterPortDriver_DBD += asyn.dbd
# CounterPortDriver_DBD += LukasWaveformReader.dbd
CounterPortDriver_DBD += register.dbd
CounterPortDriver_DBD += ycpswasyn.dbd
CounterPortDriver_DBD += yamlLoader.dbd
# CounterPortDriver_DBD += yamlReader.dbd#############
CounterPortDriver_DBD += yamlDownloader.dbd 
# CounterPortDriver_DBD += $(EPICS_MODULES)/WaveformReaderAsyn/LukasWaveformReaderApp/src/waveform.dbd

# Include dbd files from all support applications:
#CounterPortDriver_DBD += xxx.dbd

# Add all the support libraries needed by this IOC
#CounterPortDriver_LIBS += xxx

# CounterPortDriver_registerRecordDeviceDriver.cpp derives from CounterPortDriver.dbd
CounterPortDriver_SRCS += CounterPortDriver_registerRecordDeviceDriver.cpp
CounterPortDriver_SRCS += counter.cpp
CounterPortDriver_SRCS += getter.cpp
CounterPortDriver_SRCS += tank.cpp

# Build the main IOC entry point on workstation OSs.
CounterPortDriver_SRCS_DEFAULT += CounterPortDriverMain.cpp
CounterPortDriver_SRCS_vxWorks += -nil-

# Add support from base/src/vxWorks if needed
#CounterPortDriver_OBJS_vxWorks += $(EPICS_BASE_BIN)/vxComLibrary

# Finally link to the EPICS Base libraries
CounterPortDriver_LIBS += $(EPICS_BASE_IOC_LIBS)
# CounterPortDriver_LIBS += asyn
# #Is this needed here?
CounterPortDriver_LIBS += cpsw
# CounterPortDriver_LIBS += LukasWaveformReader
CounterPortDriver_LIBS += ycpswasyn
CounterPortDriver_LIBS += asyn
CounterPortDriver_LIBS += yamlLoader
# CounterPortDriver_LIBS += yamlReader
CounterPortDriver_LIBS += yamlDownloader
#===========================

USR_CPPFLAGS += -std=c++11 -Wall -g

# =========================================================================
#  Link in external package libraries (-lcentral_node_engine)
# =========================================================================
YAML_DIR=$(YAML_LIB)
CPSW_DIR=$(CPSW_LIB)
LukasWaveformReader_DIR=$(WAVEFORMREADERASYN_LIB)
USR_LDFLAGS += -L$(WAVEFORMREADERASYN_LIB)
USR_LDFLAGS += -L$(YAML_LIB)
USR_LDFLAGS += -L$(YAMLREADER_LIB)
USR_LDFLAGS += -L$(DEVICELIB_LIB)
USR_LDFLAGS += -L$(CPSW_FRAMEWORK_LIB)
USR_LDFLAGS += -L$(BOOST_LIB)


include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

tirpc_DIR         = $(TIRPC_LIB)

ifeq ($(NEEDS_TIRPC),YES)
USR_LIBS_Linux += tirpc
# USR_LDFLAGS += -L$(TIRPC_LIB)
endif