.SUFFIXES: .c .o .lo

COMPILE = $(CC) -Wall -D_FILE_OFFSET_BITS=64 -g -DDEBUG_FLAG -DOS_LINUX
INC_PATH = 
LIB_PATH = -L/usr/local/lib  -lpthread

FAST_SHARED_OBJS = hash.lo chain.lo shared_func.lo ini_file_reader.lo \
                   logger.lo sockopt.lo base64.lo sched_thread.lo \
                   http_func.lo md5.lo pthread_func.lo local_ip_func.lo \
                   avl_tree.lo

HEADER_FILES = common_define.h hash.h chain.h logger.h base64.h \
               shared_func.h pthread_func.h ini_file_reader.h _os_bits.h \
               sockopt.h sched_thread.h http_func.h md5.h local_ip_func.h \
               avl_tree.h

ALL_OBJS = $(STATIC_OBJS) $(FAST_SHARED_OBJS)

ALL_PRGS = 
ALL_LIBS = libfastcommon.so.1

all: $(ALL_OBJS) $(ALL_PRGS) $(ALL_LIBS)
libfastcommon.so.1:
	$(COMPILE) -o $@ $< -shared $(FAST_SHARED_OBJS) $(LIB_PATH)
.o:
	$(COMPILE) -o $@ $<  $(STATIC_OBJS) $(LIB_PATH) $(INC_PATH)
.c:
	$(COMPILE) -o $@ $<  $(STATIC_OBJS) $(LIB_PATH) $(INC_PATH)
.c.o:
	$(COMPILE) -c -o $@ $<  $(INC_PATH)
.c.lo:
	$(COMPILE) -c -fPIC -o $@ $<  $(INC_PATH)
install:
	cp -f $(ALL_LIBS) /usr/local/lib/
	mkdir -p /usr/local/include/fastcommon
	cp -f $(HEADER_FILES) /usr/local/include/fastcommon
	ln -fs /usr/local/lib/libfastcommon.so.1 /usr/local/lib/libfastcommon.so
	ln -fs /usr/local/lib/libfastcommon.so.1 /usr/lib/libfastcommon.so
clean:
	rm -f $(ALL_OBJS) $(ALL_PRGS) $(ALL_LIBS)

