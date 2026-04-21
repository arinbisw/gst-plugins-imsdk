cmake_minimum_required(VERSION 3.16)
project(gstreamer-qcom-oss-base-1.0
  VERSION ${GST_PLUGINS_QTI_OSS_VERSION}
  LANGUAGES C CXX
)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

include_directories(${SYSROOT_INCDIR})
link_directories(${SYSROOT_LIBDIR})

find_package(PkgConfig)

# Get the pkgconfigs exported by the automake tools
pkg_check_modules(GST REQUIRED gstreamer-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_ALLOC REQUIRED gstreamer-allocators-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_VIDEO REQUIRED gstreamer-video-1.0>=${GST_VERSION_REQUIRED})

pkg_check_modules(GST_JSON REQUIRED json-glib-1.0)
pkg_check_modules(FASTCV qcom-fastcv-binaries)
pkg_check_modules(EGL egl)
pkg_check_modules(GLES glesv2)
pkg_check_modules(OPEN_CV opencv4)
pkg_check_modules(QMMF_CAMERA_METADATA qmmf_camera_metadata)

include(CheckIncludeFile)
include(CheckIncludeFileCXX)

# Check whether MMM color format header is present.
check_include_file("display/media/mmm_color_fmt.h" HAVE_MMM_COLOR_FMT_H)

# Check whether MSM media info header is present.
check_include_file("media/msm_media_info.h" HAVE_MSM_MEDIA_INFO_H)

# Check whether DMA HEAP header is present.
check_include_file("linux/dma-heap.h" HAVE_LINUX_DMA_HEAP_H)

# Check whether Adreno C2D header is present.
check_include_file("adreno/c2d2.h" HAVE_ADRENO_C2D2_H)

# Check whether FastCV header is present.
check_include_file("fastcv/fastcv.h" HAVE_FASTCV_H)

# Check whether GBM header is present.
check_include_file("gbm_priv.h" HAVE_GBM_PRIV_H)

# Common compiler flags.
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-parameter")

# Common CXX compiler flags.
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-unused-parameter")

include_directories(
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include/gstreamer-1.0>
)

# Define path to gst-plugins-base tree
set(QTI_PLUGINS_BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

# Define the path to the common pkg-config template file used by all subdirectories
set(BASE_COMMON_PC_IN ${CMAKE_CURRENT_SOURCE_DIR}/gst/common.pc.in)

# gst/gfx: requires gstreamer-1.0, glesv2
if(GST_FOUND AND GLES_FOUND)
  add_subdirectory(gst/gfx)
else()
  message(STATUS "Skipping gst/gfx: missing dependency gstreamer-1.0 or glesv2")
endif()

# gst/utils: requires gstreamer-1.0, json-glib-1.0
if(GST_FOUND AND GST_JSON_FOUND)
  add_subdirectory(gst/utils)
else()
  message(STATUS "Skipping gst/utils: missing dependency gstreamer-1.0 or json-glib-1.0")
endif()

# gst/video: core lib always built when base GST deps are present.
# Three optional backend libs are built within the subdirectory based on
# available hardware/software dependencies:
#   gstqtivideobase-c2d    (requires adreno/c2d2.h)
#   gstqtivideobase-gles   (requires glesv2)
#   gstqtivideobase-opencv (requires opencv4)
if(GST_FOUND AND GST_ALLOC_FOUND AND GST_VIDEO_FOUND)
  add_subdirectory(gst/video)
else()
  message(STATUS "Skipping gst/video: missing dependency gstreamer-1.0, gstreamer-allocators-1.0, or gstreamer-video-1.0")
endif()

# gst/memory: requires gstreamer-1.0, gstreamer-allocators-1.0
if(GST_FOUND AND GST_ALLOC_FOUND)
  add_subdirectory(gst/memory)
else()
  message(STATUS "Skipping gst/memory: missing dependency gstreamer-1.0 or gstreamer-allocators-1.0")
endif()

# gst/ml: requires gstreamer-1.0, gstreamer-allocators-1.0, gstreamer-video-1.0
if(GST_FOUND AND GST_ALLOC_FOUND AND GST_VIDEO_FOUND)
  add_subdirectory(gst/ml)
else()
  message(STATUS "Skipping gst/ml: missing dependency gstreamer-1.0, gstreamer-allocators-1.0, or gstreamer-video-1.0")
endif()

# gst/cv: requires gstreamer-1.0
if(GST_FOUND AND OPEN_CV_FOUND)
  add_subdirectory(gst/cv)
else()
  message(STATUS "Skipping gst/cv: missing dependency gstreamer-1.0")
endif()

# gst/allocators: requires gstreamer-1.0, gstreamer-allocators-1.0
if(GST_FOUND AND GST_ALLOC_FOUND)
  add_subdirectory(gst/allocators)
else()
  message(STATUS "Skipping gst/allocators: missing dependency gstreamer-1.0 or gstreamer-allocators-1.0")
endif()

# gst/camera: requires gstreamer-1.0, gstreamer-allocators-1.0, qmmf_camera_metadata
if(GST_FOUND AND GST_ALLOC_FOUND AND QMMF_CAMERA_METADATA_FOUND)
  add_subdirectory(gst/camera)
else()
  message(STATUS "Skipping gst/camera: missing dependency gstreamer-1.0, gstreamer-allocators-1.0, or qmmf_camera_metadata")
endif()

