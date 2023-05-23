CC=gcc
CFLAGS=-I.

DEPS = libffi_tutorial.h
OBJ = main.o
LIBS=./libffi_tutorial.so

%.o: %.c $(DEPS)
	$(CC) -c -o $@ $< $(CFLAGS)

main: $(OBJ)
	$(CC) -o $@ $^ $(CFLAGS) $(LIBS)

.PHONY: clean

clean:
	rm -f *.o main
