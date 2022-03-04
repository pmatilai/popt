
include(CheckSymbolExists)
include(GNUInstallDirs)

set (popt_SOURCES
	popt.c
	poptconfig.c
	popthelp.c
	poptint.c
	poptparse.c
	poptint.h
	system.h
)

set (popt_HEADERS
	popt.h
)

add_library(popt SHARED ${popt_SOURCES})
set_target_properties(popt PROPERTIES
	PUBLIC_HEADER popt.h
	SOVERSION 0.0.1
)

function(chkdef func inc)
    string(TOUPPER ${func} FUNC)
    set(HAVENAME HAVE_${FUNC})
    check_symbol_exists(${func} "${inc}" ${HAVENAME})
    if (${HAVENAME})
        add_compile_definitions(${HAVENAME})
    endif()
endfunction()

chkdef(stpcpy string.h)
chkdef(strerror string.h)
chkdef(getuid unistd.h)
chkdef(geteuid unistd.h)
chkdef(mtrace mcheck.h)
chkdef(secure_getenv stdlib.h)
chkdef(__secure_getenv stdlib.h)
chkdef(setreuid unistd.h)
chkdef(setuid unistd.h)
chkdef(stpcpy string.h)
chkdef(strerror string)
chkdef(vasprintf stdio)
chkdef(srandom stdlib.h)
chkdef(glob_pattern_p glob.h)
chkdef(mbsrtowcs wchar.h)

# autotool compatibility stuff
add_compile_definitions(POPT_SYSCONFDIR="${CMAKE_INSTALL_FULL_SYSCONFDIR}")
add_compile_definitions(PACKAGE="${PROJECT_NAME}")

install(FILES ${popt_HEADERS} TYPE INCLUDE)
install(TARGETS popt TYPE LIBRARY)
