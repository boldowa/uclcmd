project(uclcmd C)
cmake_minimum_required(VERSION 3.10)

set(INSTALL_BIN_DIR "${CMAKE_INSTALL_PREFIX}/bin" CACHE PATH "Installation directory for executables")
set(INSTALL_LIB_DIR "${CMAKE_INSTALL_PREFIX}/lib" CACHE PATH "Installation directory for libraries")
set(INSTALL_INC_DIR "${CMAKE_INSTALL_PREFIX}/include" CACHE PATH "Installation directory for headers")
set(INSTALL_MAN_DIR "${CMAKE_INSTALL_PREFIX}/share/man" CACHE PATH "Installation directory for manual pages")
set(INSTALL_PKGCONFIG_DIR "${CMAKE_INSTALL_PREFIX}/share/pkgconfig" CACHE PATH "Installation directory for pkgconfig (.pc) files")

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBUCL libucl REQUIRED)

set(UCLCMD_SRC
	uclcmd.c
	uclcmd_common.c
	uclcmd_get.c
	uclcmd_merge.c
	uclcmd_output.c
	uclcmd_parse.c
	uclcmd_remove.c
	uclcmd_set.c
)

add_executable(uclcmd ${UCLCMD_SRC})
target_link_libraries(uclcmd ${LIBUCL_LIBRARIES})
target_include_directories(uclcmd PUBLIC ${LIBUCL_INCLUDE_DIRS})
install(TARGETS uclcmd
	RUNTIME DESTINATION "${INSTALL_BIN_DIR}"
	ARCHIVE DESTINATION "${INSTALL_LIB_DIR}"
	LIBRARY DESTINATION "${INSTALL_LIB_DIR}")

