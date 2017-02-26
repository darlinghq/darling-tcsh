project(tcsh)

include_directories(
	${CMAKE_SOURCE_DIR}/platform-include
	${CMAKE_SOURCE_DIR}/src/libc/include/FreeBSD
	${CMAKE_SOURCE_DIR}/src/libc/include/NetBSD
	${CMAKE_SOURCE_DIR}/src/libiconv/include
	${CMAKE_CURRENT_SOURCE_DIR}/tcsh
	${CMAKE_CURRENT_SOURCE_DIR}/gen
)

add_compile_options(
	-nostdinc
	-no-cpp-precomp
	#-mdynamic-no-picc Waiting for Mach-Os
	-fstack-protector-all
	-fPIC
	-Wno-everything
)

add_definitions(
	-D_PATH_TCSHELL='"/bin/tcsh"'
	-DDARWIN
)


set(CMAKE_EXE_LINKER_FLAGS "-nodefaultlibs -nostdlib -fPIC -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")

add_darling_executable(tcsh
	tcsh/sh.c
	tcsh/sh.dir.c
	tcsh/sh.dol.c
	tcsh/sh.err.c
	tcsh/sh.exec.c
	tcsh/sh.char.c
	tcsh/sh.exp.c
	tcsh/sh.file.c
	tcsh/sh.func.c
	tcsh/sh.glob.c
	tcsh/sh.hist.c
	tcsh/sh.init.c
	tcsh/sh.lex.c
	tcsh/sh.misc.c
	tcsh/sh.parse.c
	tcsh/sh.print.c
	tcsh/sh.proc.c
	tcsh/sh.sem.c
	tcsh/sh.set.c
	tcsh/sh.time.c
	tcsh/glob.c
	tcsh/mi.termios.c
	tcsh/ma.setp.c
	tcsh/vms.termcap.c
	tcsh/tw.help.c
	tcsh/tw.init.c
	tcsh/tw.parse.c
	tcsh/tw.spell.c
	tcsh/tw.comp.c
	tcsh/tw.color.c
	tcsh/ed.chared.c
	tcsh/ed.refresh.c
	tcsh/ed.screen.c
	tcsh/ed.init.c
	tcsh/ed.inputl.c
	tcsh/ed.defns.c
	tcsh/ed.xmap.c
	tcsh/ed.term.c
	tcsh/tc.alloc.c
	tcsh/tc.bind.c
	tcsh/tc.const.c
	gen/tc.defs.c
	tcsh/tc.disc.c
	tcsh/tc.func.c
	tcsh/tc.nls.c
	tcsh/tc.os.c
	tcsh/tc.printf.c
	tcsh/tc.prompt.c
	tcsh/tc.sched.c
	tcsh/tc.sig.c
	tcsh/tc.str.c
	tcsh/tc.vers.c
	tcsh/tc.who.c
)

target_link_libraries(tcsh termcap iconv)

install(TARGETS tcsh DESTINATION libexec/darling/usr/bin)

install(FILES csh.cshrc csh.login csh.logout DESTINATION libexec/darling/etc)

install(FILES tcsh.1 DESTINATION libexec/darling/usr/share/man/man1)

install(DIRECTORY locale DESTINATION libexec/darling/usr/share)
