OBJS = foo.o bar.o
PROG = foobar

%.o: %.c 
	gcc -c -g -o $@ $<  

$(PROG): $(OBJS)
	gcc -g -o $@ $^

clean:
	rm -rf $(OBJS) $(PROG)
