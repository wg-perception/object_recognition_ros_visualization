include_directories(SYSTEM ${catkin_INCLUDE_DIRS})

find_package(Qt5Core QUIET)
if(Qt5Core_FOUND)
find_package(Qt5Core)
find_package(Qt5Gui)

qt5_wrap_cpp(MOC_FILES
  ork_object_display.h
  ork_table_display.h
)
else()
find_package(Qt4 COMPONENTS QtCore QtGui QUIET)
include(${QT_USE_FILE})
add_definitions(-DQT_NO_KEYWORDS)
endif()

set(SOURCE_FILES
  ork_object_display.cpp
  ork_object_visual.cpp
  ork_table_display.cpp
  ork_table_visual.cpp
  ${MOC_FILES}
)

add_library(${PROJECT_NAME} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES}
                                           ${QT_LIBRARIES}
)
if(NOT Qt4_FOUND)
target_link_libraries(${PROJECT_NAME} Qt5::Core Qt5::Gui)
endif()

install(TARGETS ${PROJECT_NAME}
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
