include ../make.def
TARGET = appsvc
CXX = g++
CXXFLAGS = -std=c++11 -ggdb3 -Wall -O2
OEXT = o

# https://blog.csdn.net/humadivinity/article/details/78890754
# boost_thread is not needed, linked here is used to packed for cpprest 
INCLUDES = -I/usr/local/ace/include/ -I/usr/local/include
DEP_LIBS = -L../common -lcommon -L/usr/local/ace/lib/ -L/usr/local/lib -L/usr/local/lib64 -lpthread -lcrypto -lssl -lACE -lcpprest -lboost_thread -lboost_system -lboost_regex -Wl,-Bstatic -llog4cpp -ljsoncpp -Wl,-Bdynamic

all : format $(TARGET) 

## source and object files 
SRCS = \
	main.cpp \
	Application.cpp \
	ApplicationShortRun.cpp \
	ApplicationPeriodRun.cpp \
	Configuration.cpp \
	RestHandler.cpp \
	AppProcess.cpp \
	DockerProcess.cpp \
	MonitoredProcess.cpp \
	DailyLimitation.cpp \
	ResourceLimitation.cpp \
	ResourceCollection.cpp \
	LinuxCgroup.cpp \
	User.cpp \
	Role.cpp \
	TimerHandler.cpp
		

OBJS = $(SRCS:.cpp=.$(OEXT))

# =============
# File suffixes
# =============
.SUFFIXES: .cpp .$(OEXT)

# ====================
#compile all cpp files
# ===================
%.${OEXT}: %.cpp
	${CXX} ${CXXFLAGS} ${INCLUDES} -DBUILD_TAG=${BUILD_TAG} -c $<;
	# cleanup.py ${CXX} ${CXXFLAGS} ${INCLUDES} -DBUILD_TAG=${BUILD_TAG} -c $<;

# Executable binary
$(TARGET): $(OBJS) 
	$(CXX) ${CXXFLAGS} -o $@ $^ $(DEP_LIBS)

format:
	#dos2unix *.cpp *.h *.json

.PHONY: clean
clean:
	rm -f *.$(OEXT) $(TARGET) 
