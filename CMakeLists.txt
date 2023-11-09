cmake_minimum_required(VERSION 3.0)

project(xcursor-viewer LANGUAGES CXX VERSION 1.1)

# Enable C++14
set(CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 14)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt5 5.2 REQUIRED Core Gui Widgets)

set(SOURCES main.cpp dialog.cpp)
set(HEADERS dialog.h)
set(FORMS dialog.ui)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS} ${FORMS})
target_link_libraries(${PROJECT_NAME} Qt5::Core Qt5::Gui Qt5::Widgets)

install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION bin
)

include(cmake/SparkDesktopMacros.cmake)
# 内容默认应用名称: Name= 应与项目名称相同
spark_desktop_macros(
    # 应用名称: Name=
    "XCursor Viewer"
    # 应用名称: Name[zh_CN]=
    "XCursor Viewer(光标文件查看器)"
    # 应用说明: Comment=
    "XCursor Viewer"
    # 应用类型: Type=
    "Application"
    # 执行程序: Exec=
    "xcursor-viewer %f"
    # 图标路径: Icon=
    "x"
    # 应用分类: Category=
    "Utility"
)
install(FILES ${SPARK_DESKTOP_FILE}
    DESTINATION /usr/share/applications
)

# 注释行(使用方式)
find_package(SparkDebPackage PATHS ${CMAKE_SOURCE_DIR})
add_package_descript(cmake/spark-deb-package.descript)