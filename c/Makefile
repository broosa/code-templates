CC = gcc

CFLAGS := $(CFLAGS) -Wall -ggdb -std=c99

SRC_DIR = src
BUILD_DIR = build

RELEASE_SRC = src/main.c

RELEASE_EXE = bin/main.out

DEPS_FILE = build/deps.d

SRC_FILES = $(wildcard src/*.c)
SRC = $(SRC_FILES:src/%=%)
OBJ = $(SRC:.c=.o)
OBJ_FILES = $(addprefix build/,$(OBJ))

all: release

build-setup:
	@mkdir -p build

generate-depends:
	$(CC) $(CFLAGS) -MM -MP -MF $(DEPS_FILE) $(SRC_FILES)

#Depends on all object files excpet for the one that contains the test main method
#This is hacky. Fix later.
build-release: $(filter-out $(TEST_SRC:src/%.c=build/%.o), $(OBJ_FILES))
	$(CC) $(CFLAGS) -o $(RELEASE_EXE) $^

#Same for test. Includes all .o files except for the one that contains the release
#executable entry point. 
#build-test: $(filter-out $(RELEASE_SRC:src/%.c=build/%.o), $(OBJ_FILES)) 
#	$(CC) $(CFLAGS) -o $(TEST_EXE) $^
	
release: build-setup generate-depends build-release

#test: build-setup generate-depends build-test
	
-include $(DEPS_FILE)

clean:
	rm -rf ./build/*
	rm -rf ./*.out

%.c: %.o

$(BUILD_DIR)/%.o: $(SRC_DIR)/%.c
	$(CC) $(CFLAGS) -c -o "$@" $^
	
redo: clean
	main 
