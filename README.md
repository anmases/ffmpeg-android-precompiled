# Precompiled binaries for Android FFMPEG 
## version 7.0.2

This project is under development and needs to be tested.

You have to add this project as a git submodule in app/src/main/jniLibs.

Then, CMakeLists.txt must be configured to include libraries:

```cmake
set(IMPORT_DIR ${CMAKE_SOURCE_DIR}/../jniLibs)
include_directories(${IMPORT_DIR}/${ANDROID_ABI}/include)
add_library(avcodec SHARED IMPORTED)
set_target_properties(avcodec PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libavcodec.so)

add_library(avfilter SHARED IMPORTED)
set_target_properties(avfilter PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libavfilter.so)

add_library(avformat SHARED IMPORTED)
set_target_properties(avformat PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libavformat.so)

add_library(avutil SHARED IMPORTED)
set_target_properties(avutil PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libavutil.so)

add_library(swresample SHARED IMPORTED)
set_target_properties(swresample PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libswresample.so)

add_library(swscale SHARED IMPORTED)
set_target_properties(swscale PROPERTIES IMPORTED_LOCATION ${IMPORT_DIR}/${ANDROID_ABI}/libswscale.so)

target_link_libraries(
        avformat
        avcodec
        avfilter
        avutil
        swresample
        swscale
			#Rest of the libraries
)
```

It's not working for x86 due to TEXTREL x264 lib, that has to be solved.
It's tested and working fine on arm64.