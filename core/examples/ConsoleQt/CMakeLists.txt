#
# (C) Copyright 2024-2026 Johns Hopkins University (JHU), All Rights Reserved.
#
# --- begin cisst license - do not edit ---
#
# This software is provided "as is" under an open source license, with
# no warranty.  The complete license can be found in license.txt and
# http://www.cisst.org/cisst/license.txt.
#
# --- end cisst license ---

cmake_minimum_required (VERSION 3.10)
project (sawGalilConsoleQt VERSION 2.1.0)

set (REQUIRED_CISST_LIBRARIES
  cisstCommon
  cisstCommonQt
  cisstVector
  cisstVectorQt
  cisstOSAbstraction
  cisstMultiTask
  cisstMultiTaskQt
  cisstParameterTypes
  cisstParameterTypesQt
)

# find cisst and make sure the required libraries have been compiled
find_package (cisst 1.2 REQUIRED COMPONENTS ${REQUIRED_CISST_LIBRARIES})

# catkin/ROS paths
cisst_set_output_path ()

find_package (sawGalilController
  HINTS ${CMAKE_BINARY_DIR})

if (sawGalilController_FOUND)

  include_directories (${sawGalilController_INCLUDE_DIR})
  link_directories (${sawGalilController_LIBRARY_DIR})

  add_executable (sawGalilConsoleQt main.cpp)

  target_link_libraries (sawGalilConsoleQt
                         ${sawGalilController_LIBRARIES}
                         ${cisst_LIBRARIES})

  set_target_properties (sawGalilConsoleQt PROPERTIES
    COMPONENT sawGalilController-Examples
    FOLDER "sawGalilController")

  install (TARGETS sawGalilConsoleQt
    COMPONENT sawGalilController-Examples
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)

else (sawGalilController_FOUND)
  message ("Information: sawGalilConsoleQt will not be compiled, it requires sawGalilController")
endif (sawGalilController_FOUND)
