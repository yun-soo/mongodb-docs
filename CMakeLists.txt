cmake_minimum_required(VERSION 3.8.0)

project(mongodb-docs)

find_package(Doxygen REQUIRED dot)

if(NOT DOXYGEN_FOUND)
    message(FATAL_ERROR "doxygen and graphviz is required to build the documentation.")
endif()

set(H $ENV{HOME})

if(DEFINED ENV{MONGODB_ROOT})
    message(STATUS "MONGODB_ROOT is $ENV{MONGODB_ROOT}.")
    set(MONGODB_ROOT $ENV{MONGODB_ROOT})
    if(NOT EXISTS ${MONGODB_ROOT} OR NOT EXISTS ${MONGODB_ROOT}/src OR NOT EXISTS ${MONGODB_ROOT}/docs)
        message(FATAL_ERROR "MongoDB source does not exist at ${MONGODB_ROOT}.")
    endif()
elseif(EXISTS ${H}/mongo AND EXISTS ${H}/mongo/src AND EXISTS ${H}/mongo/docs)
    message(STATUS "Found MongoDB source at ${H}/mongo.")
    set(MONGODB_ROOT ${H}/mongo)
else()
    message(STATUS "Could not find MongoDB source.")
    message(STATUS "Downloading MongoDB source from github...")
    include(ExternalProject)

    ExternalProject_Add(mongodb
        GIT_REPOSITORY https://github.com/mongodb/mongo
        GIT_PROGRESS true
        STEP_TARGETS download
    )
    set(MONGODB_ROOT ${CMAKE_BINARY_DIR}/mongodb-prefix/src/mongodb)
endif()

message("MONGODB_ROOT is set to ${MONGODB_ROOT}.")

set(MONGODB_DOCS ${MONGODB_ROOT}/docs)
set(MONGODB_SRC ${MONGODB_ROOT}/src)
set(MONGODB_DOCS_OUT ${CMAKE_BINARY_DIR}/docs)

message("Generated documents will be located at ${MONGODB_DOCS_OUT}.")

set(doxyfile_in ${CMAKE_CURRENT_SOURCE_DIR}/doxyfile.in)
set(doxyfile ${CMAKE_CURRENT_BINARY_DIR}/doxyfile)

configure_file(${doxyfile_in} ${doxyfile})

message("Doxygen build started.")

add_custom_target(doc ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${doxyfile}
    VERBATIM
)
