cmake_minimum_required(VERSION 3.12)
project(minidb)

set(CMAKE_CXX_STANDARD 14)


set(Boost_USE_STATIC_LIBS        ON)
set(Boost_USE_MULTITHREADED      ON)
set(BOOST_ROOT "/usr/include/boost")

set(CMAKE_EXE_LINKER_FLAGS "-lreadline")

find_package(Boost
        COMPONENTS
        serialization
        system
        filesystem
        program_options
        regex
        )

if (Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    include_directories(${READLINE_ROOT})
    MESSAGE( STATUS "Boost_INCLUDE_DIRS = ${Boost_INCLUDE_DIRS}.")
    MESSAGE( STATUS "Boost_LIBRARIES = ${Boost_LIBRARIES}.")
    MESSAGE( STATUS "Boost_LIB_VERSION = ${Boost_LIB_VERSION}.")

    set(SOURCE_FILES
            src/block_handle.cc
            src/block_handle.h
            src/block_info.cc
            src/block_info.h
            src/buffer_manager.cc
            src/buffer_manager.h
            src/catalog_manager.cc
            src/catalog_manager.h
            src/commons.h
            src/exceptions.h
            src/file_handle.cc
            src/file_handle.h
            src/file_info.cc
            src/file_info.h
            src/index_manager.cc
            src/index_manager.h
            src/interpreter.cc
            src/interpreter.h
            src/main.cc
            src/minidb_api.cc
            src/minidb_api.h
            src/record_manager.cc
            src/record_manager.h
            src/sql_statement.cc
            src/sql_statement.h
            )

    add_executable(minidb ${SOURCE_FILES})
    link_directories(... ${Boost_LIBRARY_DIRS})
    target_link_libraries(minidb readline)
    target_link_libraries(minidb ${Boost_LIBRARIES})

else()
    MESSAGE( STATUS "没发现任何BOOST")
endif ()