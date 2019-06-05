cmake_minimum_required(VERSION 3.10)
project(MabiMe)

set(CMAKE_VERBOSE_MAKEFILE TRUE)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_CXX_FLAGS "-D _DEBUG")

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set(MABIME_HEADERS mainwindow.h
        PackReader/mabipackreader.h
        PackReader/mabimt.h
        mabimeglwidget.h
        PackReader/pmgreader.h
        PackReader/frmreader.h
        PackReader/packmanager.h
        bone.h
        model.h
        settingswindow.h
        mabimelayerdelegate.h
        Parsers/localemaphelper.h
        Parsers/xmlparser.h
        Parsers/characterstyleparser.h
        Parsers/colourparser.h
        mabimecolourdelegate.h
        aboutwindow.h
        Parsers/faceemotionparser.h
        scrollingdisabledqlistwidget.h)

set(MABIME_SOURCES main.cpp
        mainwindow.cpp
        PackReader/mabipackreader.cpp
        PackReader/mabimt.cpp
        mabimeglwidget.cpp
        PackReader/pmgreader.cpp
        PackReader/frmreader.cpp
        PackReader/packmanager.cpp
        bone.cpp
        model.cpp
        settingswindow.cpp
        mabimelayerdelegate.cpp
        Parsers/localemaphelper.cpp
        Parsers/xmlparser.cpp
        Parsers/characterstyleparser.cpp
        Parsers/colourparser.cpp
        mabimecolourdelegate.cpp
        aboutwindow.cpp
        Parsers/faceemotionparser.cpp
        scrollingdisabledqlistwidget.cpp)

set(MABIME_RESOURCES images.qrc)

set(MABIME_UI mainwindow.ui settingswindow.ui aboutwindow.ui)


IF (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_LINUX")
ENDIF (${CMAKE_SYSTEM_NAME} MATCHES "Linux")

#find_package(OpenGL REQUIRED)
#find_package(Qt4 REQUIRED)
#find_package(Qt5 REQUIRED)
find_package(Qt5Core)
if(${Qt5Core_FOUND} )
#    message(STATUS "\${Qt5Core_INCLUDE_DIRS}=${Qt5Core_INCLUDE_DIRS}")
ELSE()
    message(WARNING "Qt5Core Not Found")
ENDIF()

find_package(Qt5Widgets CONFIG REQUIRED)
if(${Qt5Widgets_FOUND} )
#    message(STATUS "\${Qt5Widgets_INCLUDE_DIRS}=${Qt5Widgets_INCLUDE_DIRS}")
ELSE()
    message(WARNING "Qt5Widgets Not Found")
ENDIF()
find_package(Qt5OpenGL REQUIRED)
if(${Qt5OpenGL_FOUND} )
#    message(STATUS "\${Qt5OpenGL_INCLUDE_DIRS}=${Qt5OpenGL_INCLUDE_DIRS}")
ELSE()
    message(WARNING "Qt5OpenGL Not Found")
ENDIF()
find_package(Qt5Xml REQUIRED)

find_package(Qt5OpenGL REQUIRED)

find_package(OpenGL REQUIRED)

add_executable(MabiMe  ${MABIME_HEADERS} ${MABIME_SOURCES} ${MABIME_UI} ${MABIME_RESOURCES})
include_directories(${OPENGL_INCLUDE_DIRS} ${Qt5OpenGL_INCLUDE_DIRS} ${Qt5Core_INCLUDE_DIRS} ${Qt5Widgets_INCLUDE_DIRS})
target_link_libraries(MabiMe ${OPENGL_LIBRARIES} Qt5::Core Qt5::Widgets Qt5::OpenGL Qt5::Xml)
