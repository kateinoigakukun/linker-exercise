foo/libfoo.a:
	clang -c foo/foo.c -o foo/foo.o
	ar -r foo/libfoo.a foo/foo.o
exec-dir/static-main:
	clang static-main.c -lfoo -Lfoo -o exec-dir/static-main
clean:
	rm foo/libfoo.a foo/foo.o exec-dir/static-main
