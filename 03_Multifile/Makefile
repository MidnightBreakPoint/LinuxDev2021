GENERATES = liboutput.so liboutput_static.a prog prog-a prog-so README
TRASH = *.o *~ test_prog*.txt

CFLAGS = -Wall

all:	README prog prog-a prog-so test


test:	prog prog-a prog-so
	./prog parm_1 > test_prog_1.txt
	./prog parm_1 parm_2 parm_3 > test_prog_3.txt


func.o:	outlib.h

%.o:	%.c
	cc $< -c -fPIC -o $@

liboutput:	fun.o const.o
	cc -shared fun.o const.o -o liboutput.so

liboutput_static:	fun.o const.o
	ar -rcs liboutput_static.a fun.o const.o

prog:	const.o fun.o prog.o
	cc $^ -o $@

prog-so:	 prog.o liboutput
	cc prog.o -o prog-so -L. -loutput

prog-a:	prog.o liboutput_static
	cc prog.o -o prog-a -L. -loutput_static

README:	prog
	./$< 2> $@

clean:
	rm -f $(TRASH)

distclean:	clean
	rm -rf $(GENERATES)
