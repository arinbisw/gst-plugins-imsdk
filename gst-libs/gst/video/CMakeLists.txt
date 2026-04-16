project(gstreamer-qcom-oss-video-1.0
  VERSION 1.0.0
  LANGUAGES C CXX
  DESCRIPTION "GStreamer QTI Video base library"
)

# ============================================================
# C2D backend library
# Requires: Adreno C2D2 header (adreno/c2d2.h)
# ============================================================
if(HAVE_ADRENO_C2D2_H)
  set(C2D_TARGET gstqtivideobase-c2d)

  add_library(${C2D_TARGET} SHARED
    c2d-video-converter.c
  )

  set_target_properties(${C2D_TARGET} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER "c2d-video-converter.h"
  )

  target_compile_definitions(${C2D_TARGET} PRIVATE
    HAVE_ADRENO_C2D2_H
    $<$<BOOL:${HAVE_MMM_COLOR_FMT_H}>:HAVE_MMM_COLOR_FMT_H>
    $<$<BOOL:${HAVE_MSM_MEDIA_INFO_H}>:HAVE_MSM_MEDIA_INFO_H>
    $<$<BOOL:${HAVE_LINUX_DMA_HEAP_H}>:HAVE_LINUX_DMA_HEAP_H>
    $<$<BOOL:${HAVE_GBM_PRIV_H}>:HAVE_GBM_PRIV_H>
  )

  target_include_directories(${C2D_TARGET} PRIVATE
    ${GST_INCLUDE_DIRS}
  )

  target_include_directories(${C2D_TARGET} INTERFACE
    $<BUILD_INTERFACE:${QTI_PLUGINS_BASE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include/gstreamer-1.0>
  )

  target_link_libraries(${C2D_TARGET} PRIVATE
    ${GST_LIBRARIES}
    ${GST_ALLOC_LIBRARIES}
    ${GST_VIDEO_LIBRARIES}
  )

  install(
    TARGETS ${C2D_TARGET}
    LIBRARY DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR}
    PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
                GROUP_EXECUTE GROUP_READ
                WORLD_EXECUTE WORLD_READ
    PUBLIC_HEADER DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_INCDIR}/gstreamer-1.0/gst/video/
  )
else()
  message(STATUS "Skipping gstqtivideobase-c2d: adreno/c2d2.h not found")
endif()

# ============================================================
# GLES backend library
# Requires: OpenGL ES (glesv2)
# ============================================================
if(GLES_FOUND)
  set(GLES_TARGET gstqtivideobase-gles)

  add_library(${GLES_TARGET} SHARED
    gles-video-converter.cc
  )

  set_target_properties(${GLES_TARGET} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER "gles-video-converter.h"
  )

  target_compile_definitions(${GLES_TARGET} PRIVATE
    HAVE_GLES2_H
    $<$<BOOL:${HAVE_MMM_COLOR_FMT_H}>:HAVE_MMM_COLOR_FMT_H>
    $<$<BOOL:${HAVE_MSM_MEDIA_INFO_H}>:HAVE_MSM_MEDIA_INFO_H>
    $<$<BOOL:${HAVE_LINUX_DMA_HEAP_H}>:HAVE_LINUX_DMA_HEAP_H>
    $<$<BOOL:${HAVE_GBM_PRIV_H}>:HAVE_GBM_PRIV_H>
  )

  target_include_directories(${GLES_TARGET} PRIVATE
    ${GST_INCLUDE_DIRS}
  )

  target_include_directories(${GLES_TARGET} INTERFACE
    $<BUILD_INTERFACE:${QTI_PLUGINS_BASE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include/gstreamer-1.0>
  )

  target_link_libraries(${GLES_TARGET} PRIVATE
    ${GST_LIBRARIES}
    ${GST_ALLOC_LIBRARIES}
    ${GST_VIDEO_LIBRARIES}
    gstqtigfxbase
  )

  install(
    TARGETS ${GLES_TARGET}
    LIBRARY DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR}
    PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
                GROUP_EXECUTE GROUP_READ
                WORLD_EXECUTE WORLD_READ
    PUBLIC_HEADER DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_INCDIR}/gstreamer-1.0/gst/video/
  )
else()
  message(STATUS "Skipping gstqtivideobase-gles: glesv2 not found")
endif()

# ============================================================
# OpenCV backend library
# Requires: OpenCV (opencv4)
# ============================================================
if(OPEN_CV_FOUND)
  set(OCV_TARGET gstqtivideobase-opencv)

  add_library(${OCV_TARGET} SHARED
    ocv-video-converter.cc
  )

  set_target_properties(${OCV_TARGET} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER "ocv-video-converter.h"
  )

  target_compile_definitions(${OCV_TARGET} PRIVATE
    HAVE_OPENCV_H
    $<$<BOOL:${HAVE_MMM_COLOR_FMT_H}>:HAVE_MMM_COLOR_FMT_H>
    $<$<BOOL:${HAVE_MSM_MEDIA_INFO_H}>:HAVE_MSM_MEDIA_INFO_H>
    $<$<BOOL:${HAVE_LINUX_DMA_HEAP_H}>:HAVE_LINUX_DMA_HEAP_H>
    $<$<BOOL:${HAVE_GBM_PRIV_H}>:HAVE_GBM_PRIV_H>
  )

  target_include_directories(${OCV_TARGET} PRIVATE
    ${GST_INCLUDE_DIRS}
    ${OPEN_CV_INCLUDE_DIRS}
  )

  target_include_directories(${OCV_TARGET} INTERFACE
    $<BUILD_INTERFACE:${QTI_PLUGINS_BASE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include/gstreamer-1.0>
  )

  target_link_libraries(${OCV_TARGET} PRIVATE
    ${GST_LIBRARIES}
    ${GST_ALLOC_LIBRARIES}
    ${GST_VIDEO_LIBRARIES}
    ${OPEN_CV_LIBRARIES}
  )

  install(
    TARGETS ${OCV_TARGET}
    LIBRARY DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR}
    PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
                GROUP_EXECUTE GROUP_READ
                WORLD_EXECUTE WORLD_READ
    PUBLIC_HEADER DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_INCDIR}/gstreamer-1.0/gst/video/
  )
else()
  message(STATUS "Skipping gstqtivideobase-opencv: opencv4 not found")
endif()

# ============================================================
# Core video library (always built)
# Contains: metadata, image pool, video utils, converter engine,
#           and FastCV backend (compiled in when available).
# Links against whichever backend libs were built above.
# ============================================================
set(TARGET_NAME gstqtivideobase)

add_library(${TARGET_NAME} SHARED
  gstimagepool.c
  gstvideoclassificationmeta.c
  gstvideolandmarksmeta.c
  video-converter-engine.c
  video-utils.c
  $<$<BOOL:${HAVE_FASTCV_H}>:fcv-video-converter.c>
)

set(TARGET_HEADERS
  gstimagepool.h
  gstvideoclassificationmeta.h
  gstvideolandmarksmeta.h
  video-converter-engine.h
  video-utils.h
)

set_target_properties(${TARGET_NAME} PROPERTIES
  PUBLIC_HEADER "${TARGET_HEADERS}"
  VERSION ${PROJECT_VERSION}
  SOVERSION ${PROJECT_VERSION_MAJOR}
)

if(FASTCV_FOUND)
  string(REGEX MATCH "^[0-9]+" FASTCV_VERSION_MAJOR ${FASTCV_VERSION})
endif()

target_compile_definitions(${TARGET_NAME} PRIVATE
  $<$<BOOL:${HAVE_MMM_COLOR_FMT_H}>:HAVE_MMM_COLOR_FMT_H>
  $<$<BOOL:${HAVE_MSM_MEDIA_INFO_H}>:HAVE_MSM_MEDIA_INFO_H>
  $<$<BOOL:${HAVE_LINUX_DMA_HEAP_H}>:HAVE_LINUX_DMA_HEAP_H>
  $<$<BOOL:${HAVE_ADRENO_C2D2_H}>:HAVE_ADRENO_C2D2_H>
  $<$<BOOL:${GLES_FOUND}>:HAVE_GLES2_H>
  $<$<BOOL:${HAVE_FASTCV_H}>:HAVE_FASTCV_H>
  $<$<BOOL:${FASTCV_FOUND}>:FASTCV_PKG_FOUND>
  $<$<BOOL:${FASTCV_FOUND}>:FASTCV_VERSION_MAJOR="${FASTCV_VERSION_MAJOR}">
  $<$<BOOL:${OPEN_CV_FOUND}>:HAVE_OPENCV_H>
  $<$<BOOL:${HAVE_GBM_PRIV_H}>:HAVE_GBM_PRIV_H>
)

target_include_directories(${TARGET_NAME} PRIVATE
  ${GST_INCLUDE_DIRS}
)

target_include_directories(${TARGET_NAME} INTERFACE
  $<BUILD_INTERFACE:${QTI_PLUGINS_BASE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include/gstreamer-1.0>
)

target_link_libraries(${TARGET_NAME} PRIVATE
  ${GST_LIBRARIES}
  ${GST_ALLOC_LIBRARIES}
  ${GST_VIDEO_LIBRARIES}
  gstqtiallocatorsbase
  # Link against whichever backend libs were built
  $<$<BOOL:${HAVE_ADRENO_C2D2_H}>:gstqtivideobase-c2d>
  $<$<BOOL:${GLES_FOUND}>:gstqtivideobase-gles>
  $<$<BOOL:${OPEN_CV_FOUND}>:gstqtivideobase-opencv>
)

install(
  TARGETS ${TARGET_NAME}
  LIBRARY DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR}
  PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
              GROUP_EXECUTE GROUP_READ
              WORLD_EXECUTE WORLD_READ
  PUBLIC_HEADER DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_INCDIR}/gstreamer-1.0/gst/video/
)

# Add destination of compiletime pkg-config file to PKG_CONFIG_PATH
set(ENV{PKG_CONFIG_PATH} "${CMAKE_CURRENT_BINARY_DIR}:$ENV{PKG_CONFIG_PATH}")

configure_file(
  ${BASE_COMMON_PC_IN}
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pc
  @ONLY
)

install(
  FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pc
  DESTINATION ${GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR}/pkgconfig
)
