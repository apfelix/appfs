#-----------------------------------------------------------------------------
# paths
#-----------------------------------------------------------------------------

SHELL		=	/bin/bash

OPT		=	opt

CC		=	gcc -Wall -Werror -fprofile-arcs -ftest-coverage
CXX		=	g++ -Wall -Werror -fprofile-arcs -ftest-coverage
OBJDIR		=	obj
BINDIR		=	bin
SRCDIR		=	.

ifeq ($(OPT),opt)
MAKE		=	-O3
else
ifeq ($(OPT),dbg)
MAKE		=	-g
else
MAKE		=	-O
endif
endif

ifeq ($(TYPE),int)
CFLAGS		=	-D INT
else
#ifeq ($(TYPE),double)
#CFLAGS		=	-D DOUBLE
#else
CFLAGS		=	-D DOUBLE
#endif
endif

MAINNAME	=	ex4


CMAINOBJ	=	allocate.o \
			ex4.o \
			probdata.o \
			reader.o \
			template.o

MAINOBJFILES	=	$(addprefix $(OBJDIR)/,$(CMAINOBJ))

#-----------------------------------------------------------------------------
# make
#-----------------------------------------------------------------------------

.PHONY: all
all:		ex4

$(OBJDIR):
		@-mkdir -p $(OBJDIR)

$(BINDIR):
		@-mkdir -p $(BINDIR)

$(OBJDIR)/%.o:	$(SRCDIR)/%.c
		@echo "-> compiling $@"
		@$(CC) -std=c99 $(MAKE) $(CFLAGS) -I $(SRCDIR) -c $< -o $@

.PHONY: ex4
ex4:		$(OBJDIR) $(BINDIR) $(MAINOBJFILES)
		@echo "-> linking $@"
		@$(CXX) $(MAKE) $(CFLAGS) -mtune=native -fomit-frame-pointer -m64 $(MAINOBJFILES) -o $(BINDIR)/$(MAINNAME)
		ln -s $(BINDIR)/$(MAINNAME) ex5

.PHONY: clean
clean:		$(OBJDIR)
ifneq ($(OBJDIR),)
		@-(rm -f $(OBJDIR)/*.o && rmdir $(OBJDIR));
		@echo "-> remove main objective files"
endif
ifneq ($(BINDIR),)
		@-(rm -f $(BINDIR)/* && rmdir $(BINDIR));
		@echo "-> remove binary"
		@echo "-> remove files"
endif
