cmake_minimum_required(VERSION 3.10)

project(popt
	VERSION 1.18
	DESCRIPTION "A command line option parsing library"
	LANGUAGES C)

add_subdirectory(src)

install(FILES popt.3 TYPE MAN)
install(FILES COPYING README TYPE DOC)
