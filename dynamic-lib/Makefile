exec-dir-without-rpath/libs/libfoo.dylib exec-dir/libs/libfoo.dylib:
	clang -c foo/foo.c -o foo/foo.o
	ld foo/foo.o -dylib \
	    -o exec-dir/libs/libfoo.dylib \
	    -install_name @rpath/libfoo.dylib
	ld foo/foo.o -dylib \
	    -o exec-dir-without-rpath/libs/libfoo.dylib \
	    -install_name libfoo.dylib
exec-dir/dynamic-main:
	clang dynamic-main.c \
	    -lfoo -Lexec-dir/libs \
	    -rpath @executable_path/libs \
	    -o ./exec-dir/dynamic-main

exec-dir-without-rpath/dynamic-main:
	clang dynamic-main.c \
	    -lfoo -Lexec-dir-without-rpath/libs \
	    -o ./exec-dir-without-rpath/dynamic-main

.PHONY: all
all: exec-dir-without-rpath/libs/libfoo.dylib exec-dir/libs/libfoo.dylib exec-dir/dynamic-main exec-dir-without-rpath/dynamic-main

clean:
	rm -f \
	    foo/foo.o \
	    exec-dir/dynamic-main \
	    exec-dir/libs/libfoo.dylib \
	    exec-dir-without-rpath/dynamic-main \
	    exec-dir-without-rpath/libs/libfoo.dylib
