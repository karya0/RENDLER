# Prefix where Mesos is installed
MESOS_PREFIX = /usr
#MESOS_PREFIX = $(HOME)/usr

CXX = g++
CXXFLAGS = -g -g2 -O2 -std=c++11
LDFLAGS = -L$(MESOS_PREFIX)/lib
INCLUDES = -I$(MESOS_PREFIX)/include

LDFLAGS += -lmesos -lprotobuf -lpthread
CXXCOMPILE = $(CXX) $(INCLUDES) $(CXXFLAGS) -c -o $@
CXXLINK = $(CXX) $(INCLUDES) $(CXXFLAGS) -o $@ $< $(LDFLAGS)

default: all
all: rendler rendler_skeleton crawl_executor render_executor

HEADERS = rendler_helper.hpp

crawl_executor: crawl_executor.cpp $(HEADERS)
	$(CXXLINK) -lboost_regex -lcurl

%: %.cpp $(HEADERS)
	$(CXXLINK)

check: crawl
	./crawl http://mesosphere.io/team/

clean:
	(rm -f core crawl_executor render_executor rendler rendler_skeleton)
