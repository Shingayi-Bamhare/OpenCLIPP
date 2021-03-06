
TARGET := Demo
INC := -I../include
LIBS := -lOpenCLIPP-C++ -lOpenCL
SRCEXT := cpp
SRCDIR := .
BUILDDIR := build

CC := g++
CFLAGS := -g -O3 -Wall -c -fmessage-length=0 -std=c++0x
LDFLAGS := -g -L..
RM := rm -rf

SOURCES := $(shell find $(SRCDIR) -type f -name '*.$(SRCEXT)')
OBJECTS := $(patsubst $(SRCDIR)/%,$(BUILDDIR)/%,$(SOURCES:.$(SRCEXT)=.o))
DEPS := $(OBJECTS:.o=.deps)

all: $(TARGET)

$(TARGET): $(OBJECTS)
	@echo 'Building target: $@'
	@echo 'Invoking: Linker'
	$(CC) $(LDFLAGS) $^ -o $(TARGET) $(LIBS)
	@echo 'Finished building target: $@'
	@echo ' '

$(BUILDDIR)/png/%.o: $(SRCDIR)/png/%.$(SRCEXT)
	@mkdir -p $(BUILDDIR)/png
	@echo 'Building file: $<'
	$(CC) $(CFLAGS) $(INC) -MMD -MP -MF"$(@:.o=.deps)" -MT"$(@:.o=.deps)" -o "$@" "$<"
	@echo 'Finished building: $<'
	@echo ' '

$(BUILDDIR)/%.o: $(SRCDIR)/%.$(SRCEXT)
	@mkdir -p $(BUILDDIR)
	@echo 'Building file: $<'
	$(CC) $(CFLAGS) $(INC) -MMD -MP -MF"$(@:.o=.deps)" -MT"$(@:.o=.deps)" -o "$@" "$<"
	@echo 'Finished building: $<'
	@echo ' '

clean:
	@echo "Cleaning"
	$(RM) $(BUILDDIR) $(TARGET)
	@echo ' '

.PHONY: all clean
