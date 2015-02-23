CC = g++

CFLAGS := $(CFLAGS) -Wall -ggdb

SRC_DIR = src
BUILD_DIR = build
BIN_DIR = bin

DEPS_FILE = build/deps.d

TARGET_FILE_NAMES = src/main.cpp src/statexam.cpp src/stattest.cpp

SRC_FILES = $(filter-out $(TARGET_FILE_NAMES),$(wildcard src/*.cpp))

SRC = $(SRC_FILES:src/%=%)
OBJ = $(SRC:%.cpp=%.o)
OBJ_FILES = $(addprefix $(BUILD_DIR)/,$(OBJ))

all: main

build-setup:

	@mkdir -p build
	@mkdir -p bin

build-depends:
	$(CC) $(CFLAGS) -MM -MP -MF $(DEPS_FILE) $(SRC_FILES)

build-exe: $(OBJ_FILES)
	$(CC) $(CFLAGS) -o $(BIN_DIR)/$(notdir $(TGT_SRC:%.cpp=%)) $(TGT_SRC) $^

setup: build-setup build-depends
	
main: override TGT_SRC = src/main.cpp
main: setup build-exe
	
-include $(DEPS_FILE)

clean:
	rm -rf ./bin/*
	rm -rf ./build/*
	rm -rf ./*.out

$(BUILD_DIR)/%.o: $(SRC_DIR)/%.cpp
	$(CC) $(CFLAGS) -c -o "$@" $^

redo: clean
	main 
