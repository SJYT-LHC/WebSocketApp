#*****************************************************************************
# Copyright        :  
#
# Author           :   
# Date             :   
# Version          :   
# Description      :   编译命令
#
#****************************************************************************/

SHELL = /bin/sh
INC_DIR = ./
SRC_DIR = ./
OBJ_DIR = ./obj
BIN_DIR = ./bin
LIB_DIR = ./lib

$(shell mkdir -p ${OBJ_DIR})
$(shell mkdir -p ${LIB_DIR})
$(shell mkdir -p ${BIN_DIR})

SRCS = $(wildcard ${SRC_DIR}/*.cpp)
P_SRCS = $(wildcard ../proto/*.cc)
OBJ = $(patsubst %.cpp,${OBJ_DIR}/%.o,$(notdir ${SRCS}))
P_OBJ = $(patsubst %.cc,${OBJ_DIR}/%.o,$(notdir ${P_SRCS}))

BIN_OBJECT = ${BIN_DIR}/WebSocketClient

CC = g++
AR = ar rc
SHARED = -shared -o
FPIC = -fPIC -c
RDY = -rdynamic -s
CFLAGS = -g -Wall  -I/usr/local/protobuf2.6.1/include/ -I../proto/ -DASIO_STANDALONE
LIBS = -lpthread  -L/usr/local/protobuf2.6.1/lib/ -lprotobuf

all:$(BIN_OBJECT)

${BIN_OBJECT}:${OBJ} ${P_OBJ}
	$(CC)  $(OBJ) ${P_OBJ}  -o $@ $(LIBS)
${OBJ_DIR}/%.o:${SRC_DIR}/%.cpp
	$(CC) $(CFLAGS) -c  $< -o $@ 
${OBJ_DIR}/%.o:../proto/%.cc
	$(CC) $(CFLAGS) -c  $< -o $@ 

proto:
	@protoc -I:./../proto --cpp_out=../proto/  ../proto/*.proto
	
.PHONY:clean
clean:
	find ${OBJ_DIR} -name *.o | rm -rf
	rm $(BIN_OBJECT)
