AUTOMAKE_OPTIONS = foreign
ACLOCAL_AMFLAGS = ${ACLOCAL_FLAGS}
#SUBDIRS = tests
if WITH_GTK
bin_PROGRAMS = ansvif find_suid generic_buffer_overflow string_format ansvif_gtk
endif
if WITH_SYSCALLS
bin_PROGRAMS = ansvif find_suid generic_buffer_overflow string_format syscalls
else
bin_PROGRAMS = ansvif find_suid generic_buffer_overflow string_format
endif
noinst_LIBRARIES = libgzstream.a
libgzstream_a_SOURCES = include/gzstream/gzstream.h include/gzstream/gzstream.C
ansvif_SOURCES = src/log.cpp src/common.cpp src/bin2hex.cpp src/popen2.cpp src/main.cpp src/help.cpp src/match_fault.cpp src/sys_string.cpp src/man_read.cpp src/trash.cpp src/randomizer.cpp include/gzstream/gzstream.h include/xmlwriter/xml_writer.hpp src/version.h
if OS_IS_REDHAT
ansvif_LDADD = -lgzstream -lcryptopp -lstdc++ -lpthread -lz -L.
ansvif_CPPFLAGS = -O3 -D __REDHAT -Wall -std=c++11
ansvif_LDFLAGS = -I./include/gzstream -I./include/xml_writer -I./src/linux
endif
if OS_IS_DEBIAN
ansvif_LDADD = -lgzstream -lcrypto++ -lstdc++ -lpthread -lz -L.
ansvif_CPPFLAGS = -O3 -D __DEBIAN -Wall -std=c++11
ansvif_LDFLAGS = -I./include/gzstream -I./include/xml_writer -I./src/linux
endif
if OS_IS_FREEBSD
ansvif_LDADD = -lstdc++ -lz -L.
ansvif_LDFLAGS = -I./include/gzstream -I./include/xml_writer -I./src/linux -pthread
ansvif_CPPFLAGS = -O3 -D __DEBIAN -D __FREEBSD -Wl,--no-as-needed -std=c++11
else
ansvif_LDADD = -lestdc++ -lz -L.
ansvif_LDFLAGS = -I./include/gzstream -I./include/xml_writer -I./src/linux -pthread
ansvif_CPPFLAGS = -O3 -D __DEBIAN -Wl,--no-as-needed -std=c++11
endif
find_suid_SOURCES = src/linux/find_suid.cpp
#buffer_overflow_SOURCES = src/buffer_overflow.c
#buffer_overflow_CFLAGS = -ansi -fno-stack-protector -D_GNU_SOURCE -Wno-implicit-function-declarationw
string_format_SOURCES = src/string_format.c
string_format_CFLAGS = -ansi -D_GNU_SOURCE -Wno-format-security
generic_buffer_overflow_SOURCES = src/generic_buffer_overflow.c
if WITH_SYSCALLS
syscalls_SOURCES = src/linux/syscalls.cpp
syscalls_CPPFLAGS = -ansi -Wno-unused-result -Wno-nonnull -std=c++11
endif
if WITH_GTK
ansvif_gtk_SOURCES = src/gtk.cpp src/popen2.cpp
ansvif_gtk_LDADD = @GTK_LIBS@
ansvif_gtk_CPPFLAGS = @GTK_CFLAGS@ -fpermissive
endif
ansvifdir = bin
check: all
	./ansvif -t examples/space.txt -c ./generic_buffer_overflow -b 64 -o checkfaulty && rm checkfaulty.*
	@echo "*** CHECK 1 PASSED ***"
	./ansvif -t examples/space.txt -c ./generic_buffer_overflow -b 64
	@echo "*** CHECK 2 PASSED ***"
	./ansvif -t examples/space.txt -c ./string_format -b 32
	@echo "*** CHECK 3 PASSED ***"
	@echo "*** ALL TESTS PASSED ***"
