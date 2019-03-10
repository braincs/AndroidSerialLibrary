# 设置cmake最低版本
cmake_minimum_required(VERSION 3.4.1)


# 添加include目录路径
include_directories( ${CMAKE_SOURCE_DIR}/src/main/jni)



add_library( android_serial

             SHARED

             ${CMAKE_SOURCE_DIR}/src/main/jni/SerialPort.c
             ${CMAKE_SOURCE_DIR}/src/main/jni/sercd.c
             ${CMAKE_SOURCE_DIR}/src/main/jni/android.c
             ${CMAKE_SOURCE_DIR}/src/main/jni/unix.c
             )

target_link_libraries(
                      android_serial

                      -llog

                     )