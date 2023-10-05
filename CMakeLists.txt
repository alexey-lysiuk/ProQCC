cmake_minimum_required(VERSION 3.0)

project(proqcc LANGUAGES C)

add_executable(${PROJECT_NAME} 
	src/cmdlib.c
	src/cmdlib.h
	src/decomp.c
	src/decomp.h	
	src/pr_comp.c
	src/pr_comp.h
	src/pr_lex.c
	src/qcc.c
	src/qcc.h
	src/screen.c
	src/screen.h
)

if(MSVC)
	target_compile_definitions(${PROJECT_NAME} PRIVATE _CRT_SECURE_NO_WARNINGS)
	set(CMAKE_C_FLAGS "/MP ${CMAKE_C_FLAGS}")
else()
	target_compile_definitions(${PROJECT_NAME} PRIVATE UNIX)

	find_package(Curses REQUIRED)
	target_include_directories(${PROJECT_NAME} PRIVATE "${CURSES_INCLUDE_DIR}")
	target_link_libraries(${PROJECT_NAME} PRIVATE "${CURSES_LIBRARIES}")
endif()
