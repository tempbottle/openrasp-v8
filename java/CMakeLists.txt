cmake_minimum_required(VERSION 3.12.0)

project(java LANGUAGES CXX)

#find_package(JNI)
set(JNI_INCLUDE_DIRS "/Library/Java/JavaVirtualMachines/jdk-15.jdk/Contents/Home/include")
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} SRCS)
add_library(openrasp_v8_java SHARED ${SRCS})
target_include_directories(openrasp_v8_java PUBLIC ${JNI_INCLUDE_DIRS} ${JNI_INCLUDE_DIRS}/darwin)
add_dependencies(openrasp_v8_java base prebuilts)
target_link_libraries(openrasp_v8_java PUBLIC base prebuilts)

if (CMAKE_SYSTEM_NAME STREQUAL "Linux")
  target_link_libraries(openrasp_v8_java PRIVATE "-z noexecstack")
endif()
