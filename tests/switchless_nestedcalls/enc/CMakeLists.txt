# Copyright (c) Open Enclave SDK contributors.
# Licensed under the MIT License.

set(EDL_FILE ../switchless_nestedcalls.edl)

add_custom_command(
  OUTPUT switchless_nestedcalls_t.h switchless_nestedcalls_t.c
  DEPENDS ${EDL_FILE} edger8r
  COMMAND
    edger8r --trusted ${EDL_FILE} --search-path ${PROJECT_SOURCE_DIR}/include
    --search-path ${CMAKE_CURRENT_SOURCE_DIR})

add_enclave(
  TARGET
  switchless_nestedcalls_enc
  UUID
  d497e154-9e8e-4029-a53d-c0a36533fb95
  SOURCES
  enc.c
  ${CMAKE_CURRENT_BINARY_DIR}/switchless_nestedcalls_t.c)

enclave_include_directories(switchless_nestedcalls_enc PRIVATE
                            ${CMAKE_CURRENT_BINARY_DIR})
enclave_link_libraries(switchless_nestedcalls_enc oelibc)
