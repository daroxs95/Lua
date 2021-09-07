cmake_minimum_required(VERSION 3.1)
project(lua LANGUAGES C VERSION 5.4.3)

option(LUA_SUPPORT_DL "Support dynamic loading of compiled modules" OFF)
option(LUA_BUILD_AS_CXX "Build lua as C++" OFF)
enable_language(CXX)

if(${PROJECT_NAME} STREQUAL ${CMAKE_PROJECT_NAME})
    set(TOP_LEVEL TRUE)
else()
    set(TOP_LEVEL FALSE)
endif()

if(TOP_LEVEL)
    option(LUA_BUILD_BINARY "Build lua binary" ON)
    option(LUA_BUILD_COMPILER "Build luac compiler" ON)
else()
    option(LUA_BUILD_BINARY "Build lua binary" OFF)
    option(LUA_BUILD_COMPILER "Build luac compiler" ON)
endif()


add_subdirectory(lua-5.4.3)


include(GNUInstallDirs)

install(TARGETS lua_static
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    OBJECTS DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

#installing headers
install(DIRECTORY "./lua-5.4.3/include/" # source directory
        DESTINATION "include" # target directory
        FILES_MATCHING # install only matched files
        PATTERN "*.h" # select header files
        PATTERN "*.hpp" # select header files
        #PATTERN "*.c" # select header files
        #PATTERN "*.cpp" # select header files
)