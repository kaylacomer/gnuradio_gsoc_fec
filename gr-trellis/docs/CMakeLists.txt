# Copyright 2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# SPDX-License-Identifier: GPL-3.0-or-later
#

include(GrPython)

########################################################################
# Generate HTML doc with xmlto
########################################################################
find_program(XMLTO_EXECUTABLE xmlto)


########################################################################
# Generate xml doc
########################################################################
add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/test_tcm.py.xml
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/test_tcm.py
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/make_numbered_listing.py
    COMMAND ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/make_numbered_listing.py
            ${CMAKE_CURRENT_SOURCE_DIR}/test_tcm.py)

add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/test_viterbi_equalization1.py.xml
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/test_viterbi_equalization1.py
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/make_numbered_listing.py
    COMMAND ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/make_numbered_listing.py
            ${CMAKE_CURRENT_SOURCE_DIR}/test_viterbi_equalization1.py)

add_custom_target(
    gr_trellis_xml ALL
    DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/test_tcm.py.xml
            ${CMAKE_CURRENT_BINARY_DIR}/test_viterbi_equalization1.py.xml)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/test_tcm.py.xml
              ${CMAKE_CURRENT_BINARY_DIR}/test_viterbi_equalization1.py.xml
        DESTINATION ${GR_PKG_DOC_DIR}/xml)
