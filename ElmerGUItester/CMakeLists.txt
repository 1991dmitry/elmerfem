PROJECT(ElmerGUItester CXX)
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
FIND_PACKAGE(Qt4 COMPONENTS QtGui QtCore REQUIRED)
SET(CMAKE_INCLUDE_CURRENT_DIR ON)
SET(CMAKE_AUTOMOC ON)
SET(CMAKE_AUTORCC ON)
SET(CMAKE_AUTOUIC ON)

SET(TARGETS ElmerGUItester)

SET(HEADERS src/tester.h)
SET(FORMS forms/mainform.ui)
SET(SOURCES src/main.cpp src/tester.cpp)

SET(RESOURCES ElmerGUItester.qrc)
SET(WIN32_RC_FILE ElmerGUItester.rc)


QT4_WRAP_UI(UI_HEADERS ${FORMS})
QT4_ADD_RESOURCES(UI_RESOURCES ${RESOURCES})
INCLUDE(${QT_USE_FILE})
ADD_DEFINITIONS(${QT_DEFINITIONS})

IF(MINGW AND WIN32)
  SET(CMAKE_RC_COMPILER_INIT windres)
  ENABLE_LANGUAGE(RC)
  SET(CMAKE_RC_COMPILE_OBJECT
    "<CMAKE_RC_COMPILER> <FLAGS> -O coff <DEFINES> -i <SOURCE> -o <OBJECT>")
  SET(SOURCES ${SOURCES} ${WIN32_RC_FILE})
ENDIF()

INCLUDE_DIRECTORIES(${APPLICATION_INCLUDE_DIRS})
ADD_EXECUTABLE(ElmerGUItester WIN32 ${SOURCES} ${UI_HEADERS} ${UI_RESOURCES})
TARGET_LINK_LIBRARIES(ElmerGUItester ${QT_LIBRARIES})
INSTALL(TARGETS ElmerGUItester RUNTIME DESTINATION "bin" COMPONENT "elmergui")
