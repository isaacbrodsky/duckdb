cmake_minimum_required(VERSION 2.8.12)

project(H3Extension)

include_directories(include)
add_subdirectory(h3_functions)

set(H3_EXTENSION_FILES
    h3-extension.cpp
    h3_common.cpp
    h3_functions/h3_valid.cpp
    h3_functions/h3_cell_to_parent.cpp)

add_library(h3_extension STATIC ${H3_EXTENSION_FILES})

build_loadable_extension(h3 ${H3_EXTENSION_FILES})

find_library(H3_LIB h3)
target_link_libraries(h3_extension PUBLIC h3)

install(
  TARGETS h3_extension
  EXPORT "${DUCKDB_EXPORT_SET}"
  LIBRARY DESTINATION "${INSTALL_LIB_DIR}"
  ARCHIVE DESTINATION "${INSTALL_LIB_DIR}")
