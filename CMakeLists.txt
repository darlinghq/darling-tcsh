project(tcsh)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/tcsh
	${CMAKE_CURRENT_SOURCE_DIR}/gen
)

add_compile_options(
	-nostdinc
	-no-cpp-precomp
	-mdynamic-no-picc
	-fstack-protector-all
	-fPIC
	-Wno-everything
)

add_compile_definitions(
	_PATH_TCSHELL="/bin/tcsh"
	DARWIN
)

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
	tcsh/dotlock.c
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

target_link_libraries(tcsh system ncurses iconv)

include(InstallSymlink)

install(TARGETS tcsh DESTINATION libexec/darling/bin)
InstallSymlink(tcsh "${CMAKE_INSTALL_PREFIX}/libexec/darling/bin/csh")

install(FILES csh.cshrc csh.login csh.logout DESTINATION libexec/darling/private/etc)

install(FILES tcsh/tcsh.man DESTINATION libexec/darling/usr/share/man/man1 RENAME tcsh.1)

# meow
set(CATS
	"C"         "C"
	"et"        "et"
	"finnish"   "fi"
	"french"    "fr"
	"german"    "de"
	"greek"     "gr"
	"italian"   "it"
	"ja"        "ja"
	"pl"        "pl"
	"russian"   "ru"
	"spanish"   "es"
	"ukrainian" "ru_UA"
)

while(CATS)
	list(GET CATS 0 cat_gen_name)
	list(GET CATS 1 cat_install_dir_name)
	install(
		FILES gen/nls/${cat_gen_name}.cat
		DESTINATION libexec/darling/usr/share/local/${cat_install_dir_name}/LC_MESSAGES
		RENAME tcsh.cat
	)
	list(REMOVE_AT CATS 0 1)
endwhile()
