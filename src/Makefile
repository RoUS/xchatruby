RUBY=ruby
CC=gcc
CFLAGS=-g -Wall -O1

ARCHDIR=`$(RUBY) -rrbconfig -e "puts Config::CONFIG['archdir']"`

.SUFFIXES: .c .o .rb .h

.rb.h:
	$(RUBY) ../scripts/embedify.rb $*.rb $*.h

.c.o:
	$(CC) $(CFLAGS) -c -I$(ARCHDIR) $*.c -o $*.o

xchat-ruby.so: xchat-ruby.o xchat-ruby-plugin.h
	$(CC) -L$(ARCHDIR) $(CFLAGS) -shared -o xchat-ruby.so xchat-ruby.o -lruby

install: xchat-ruby.so
	mkdir -p ~/.xchat2
	cp xchat-ruby.so ~/.xchat2
	$(RUBY) -e 'puts $$LOAD_PATH.join("\n")' > ~/.xchat2/rubyenv

clean:
	rm -f *.so *.o xchat-ruby-plugin.h

xchat-ruby.o: xchat-ruby-plugin.h
