#
# (C) Copyright 2024 Johns Hopkins University (JHU), All Rights Reserved.
#
# --- begin cisst license - do not edit ---
#
# This software is provided "as is" under an open source license, with
# no warranty.  The complete license can be found in license.txt and
# http://www.cisst.org/cisst/license.txt.
#
# --- end cisst license ---

add_subdirectory (ConsoleTest)

if (CISST_HAS_QT)
  option (BUILD_ConsoleQt "Compile sawConsoleQt (requires Qt)" ON)
else ()
  message (STATUS "sawConsoleQt not available (requires Qt)")
endif ()

if (BUILD_ConsoleQt)
  add_subdirectory (ConsoleQt)
endif ()
