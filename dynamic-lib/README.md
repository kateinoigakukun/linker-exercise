## dynamic-lib
```sh
$ make all
```

`dyld` finds runtime libraries using `DYLD_LIBRARY_PATH` or `rpath` or something.

```sh
$ otool -L exec-dir-without-rpath/dynamic-main
exec-dir-without-rpath/dynamic-main:
	libfoo.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.250.1)
$ ./exec-dir-without-rpath/dynamic-main
dyld: Library not loaded: libfoo.dylib
  Referenced from: /Users/katei/projects/linker-exercise/dynamic-lib/./exec-dir-without-rpath/dynamic-main
  Reason: image not found
zsh: abort      ./exec-dir-without-rpath/dynamic-main
$ DYLD_LIBRARY_PATH=./exec-dir-without-rpath/libs ./exec-dir-without-rpath/dynamic-main
```

```sh
$ otool -L exec-dir/dynamic-main
exec-dir/dynamic-main:
	@rpath/libfoo.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.250.1)
$ ./exec-dir/dynamic-main$
```
