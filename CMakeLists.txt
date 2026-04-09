cmake_minimum_required(VERSION 3.16)
project(gst-plugins-qti-oss LANGUAGES C CXX)
set(GST_VERSION_REQUIRED "1.16")

# Common point for setting version of all libs of gst-plugins-qcom package
set(GST_PLUGINS_QTI_OSS_VERSION "1.0")

set(GST_PLUGINS_QTI_OSS_INSTALL_BINDIR "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_BINDIR}")
set(GST_PLUGINS_QTI_OSS_INSTALL_LIBDIR "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}")
set(GST_PLUGINS_QTI_OSS_INSTALL_INCDIR "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_INCLUDEDIR}")
set(GST_PLUGINS_QTI_OSS_INSTALL_CONFIG "${CMAKE_INSTALL_SYSCONFDIR}/configs")

option(ENABLE_GST_IMSDK_PLUGINS "Enable IMSDK Plugins" OFF)

option(ENABLE_GST_CAMERA_PLUGINS "Enable Camera Plugins" OFF) # not enabled in opensource mainline
option(ENABLE_GST_EXT_SOFTWARE_PLUGINS "Enable Software plugins depends on external software" ${ENABLE_GST_IMSDK_PLUGINS})
option(ENABLE_GST_MESSAGING_PLUGINS "Enable Messaging plugins" ${ENABLE_GST_IMSDK_PLUGINS})
option(ENABLE_GST_ML_PLUGINS "Enable ML Plugins" ${ENABLE_GST_IMSDK_PLUGINS})
option(ENABLE_GST_VIDEOPROC_PLUGINS "Enable Video processing plugins" ${ENABLE_GST_IMSDK_PLUGINS})
option(ENABLE_GST_SOFTWARE_PLUGINS "Enable Software plugins" ${ENABLE_GST_IMSDK_PLUGINS})

# Camera plugins
option(ENABLE_GST_PLUGIN_CAMIMGREPROC "Enable sys/camimgreproc" ${ENABLE_GST_CAMERA_PLUGINS})
option(ENABLE_GST_PLUGIN_CAMREPROC "Enable sys/camreproc" ${ENABLE_GST_CAMERA_PLUGINS})
option(ENABLE_GST_PLUGIN_JPEGENC "Enable sys/jpegenc" ${ENABLE_GST_CAMERA_PLUGINS})
option(ENABLE_GST_PLUGIN_QMMFSRC "Enable sys/qmmfsrc" ${ENABLE_GST_CAMERA_PLUGINS})

# External Software Plugins
option(ENABLE_GST_PLUGIN_REDISSINK "Enable ext/redissink" ${ENABLE_GST_EXT_SOFTWARE_PLUGINS})

# Messaging Plugins
option(ENABLE_GST_PLUGIN_MSGBROKER "Enable gst/msgbroker" ${ENABLE_GST_MESSAGING_PLUGINS})

# ML Plugins
option(ENABLE_GST_PLUGIN_METAMUX "Enable gst/metamux" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_METATRANSFORM "Enable gst/metatransform" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLACONVERTER "Enable ext/mlaconverter" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLDEMUX "Enable gst/mldemux" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLMETAEXTRACTOR "Enable gst/mlmetaextractor" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLMETAPARSER "Enable gst/mlmetaparser" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLPOSTPROCESS "Enable gst/mlpostprocess" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLQNN "Enable ext/mlqnn" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLSNPE "Enable ext/mlsnpe" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLTFLITE "Enable ext/mltflite" OFF) # not enabled in opensource mainline
option(ENABLE_GST_PLUGIN_MLONNX "Enable ext/mlonnx" OFF)
option(ENABLE_GST_PLUGIN_MLTOOLS "Enable tools/mltools" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_MLVCONVERTER "Enable gst/mlvconverter" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_OBJTRACKER "Enable gst/objtracker" ${ENABLE_GST_ML_PLUGINS})
option(ENABLE_GST_PLUGIN_RESTRICTED_ZONE "Enable ext/restricted-zone" ${ENABLE_GST_ML_PLUGINS})

# Video Processing plugins
option(ENABLE_GST_PLUGIN_VCOMPOSER "Enable gst/vcomposer" ${ENABLE_GST_VIDEOPROC_PLUGINS})
option(ENABLE_GST_PLUGIN_VOVERLAY "Enable gst/voverlay" ${ENABLE_GST_VIDEOPROC_PLUGINS})
option(ENABLE_GST_PLUGIN_VSPLIT "Enable gst/vsplit" ${ENABLE_GST_VIDEOPROC_PLUGINS})
option(ENABLE_GST_PLUGIN_VTRANSFORM "Enable gst/vtransform" ${ENABLE_GST_VIDEOPROC_PLUGINS})

# Software Plugins
option(ENABLE_GST_PLUGIN_BATCH "Enable gst/batch" ${ENABLE_GST_SOFTWARE_PLUGINS})
option(ENABLE_GST_PLUGIN_RTSPBIN "Enable gst/rtspbin" ${ENABLE_GST_SOFTWARE_PLUGINS})
option(ENABLE_GST_PLUGIN_SMARTVENCBIN "Enable sys/smartvencbin" ${ENABLE_GST_SOFTWARE_PLUGINS})
option(ENABLE_GST_PLUGIN_SOCKET "Enable gst/socket" ${ENABLE_GST_SOFTWARE_PLUGINS})
option(ENABLE_GST_PLUGIN_VIDEOTEMPLATE "Enable gst/videotemplate" ${ENABLE_GST_SOFTWARE_PLUGINS})

# Sample Apps and Test Framework
option(ENABLE_GST_PLUGIN_EXAMPLES "Enable examples/plugin-examples" OFF)
option(ENABLE_GST_PYTHON_EXAMPLES "Enable examples/python" OFF)
option(ENABLE_GST_SAMPLE_APPS "Enable examples/sample-apps" OFF)
option(ENABLE_GST_PLUGIN_TOOLS "Enable tools/gst-plugin-tools" OFF)
option(ENABLE_GST_TEST_FRAMEWORK "Enable tests/test-framework" OFF)
option(ENABLE_GST_UMD_DAEMON "Enable sys/umd-daemon" OFF)

# Old ML Plugins
option(ENABLE_GST_PLUGIN_MLVDETECTION "Enable ext/mlvdetection" OFF)
option(ENABLE_GST_PLUGIN_MLVPOSE "Enable ext/mlvpose" OFF)
option(ENABLE_GST_PLUGIN_MLVSEGMENTATION "Enable ext/mlvsegmentation" OFF)
option(ENABLE_GST_PLUGIN_MLVSUPERRESOLUTION "Enable ext/mlvsuperresolution" OFF)

# ACK SP Plugins
option(ENABLE_GST_PLUGIN_DFS "Enable sys/dfs" OFF)
option(ENABLE_GST_PLUGIN_DNGPACKER "Enable sys/dngpacker" OFF)
option(ENABLE_GST_PLUGIN_HEIFMUX "Enable ext/heifmux" OFF)
option(ENABLE_GST_PLUGIN_HEXAGON "Enable sys/hexagon" OFF)
option(ENABLE_GST_PLUGIN_JPEGPACKER "Enable sys/jpegpacker" OFF)
option(ENABLE_GST_PLUGIN_MLAIC "Enable ext/mlaic" OFF)
option(ENABLE_GST_PLUGIN_OVERLAY "Enable gst/overlay" OFF)

# === Enable exclude from all for internal dependncies ===
set(ENABLE_EXCLUDE_FROM_ALL "EXCLUDE_FROM_ALL")

# gst-libs is common for majority of the plugins, hence enabled by default
add_subdirectory(gst-libs)

# ============================================================
# Dependency checks for gst/ plugins
# ============================================================
find_package(PkgConfig)

# Standard GStreamer packages
pkg_check_modules(GST gstreamer-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_BASE gstreamer-base-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_ALLOC gstreamer-allocators-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_VIDEO gstreamer-video-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_AUDIO gstreamer-audio-1.0>=${GST_VERSION_REQUIRED})
pkg_check_modules(GST_RTSP gstreamer-rtsp-server-1.0>=${GST_VERSION_REQUIRED})

# Optional external packages
pkg_check_modules(CAIRO cairo)

# QTI OSS base libraries (built by gst-libs)
pkg_check_modules(GST_QCOM_UTILS gstreamer-qcom-oss-utils-1.0>=1.0.0)
pkg_check_modules(GST_QCOM_VIDEO gstreamer-qcom-oss-video-1.0>=1.0.0)
pkg_check_modules(GST_QCOM_ALLOC gstreamer-qcom-oss-allocators-1.0>=1.0.0)
pkg_check_modules(GST_QCOM_ML gstreamer-qcom-oss-ml-1.0>=1.0.0)
pkg_check_modules(GST_QCOM_MEM gstreamer-qcom-oss-memory-1.0>=1.0.0)
pkg_check_modules(GST_QCOM_CV gstreamer-qcom-oss-cv-1.0>=1.0.0)

# ============================================================
# Helper function to add sub-dir when option is set and all
# listed dependency variables evaluate to TRUE.
# Usage: add_plugin_if(<option_var> <plugin_dir> [DEP_VAR ...])
# ============================================================
function(add_plugin_if option_var plugin_dir)
  if(NOT (DEFINED ${option_var} AND ${option_var}))
    return()
  endif()
  set(deps_ok TRUE)
  set(missing_deps "")
  foreach(dep_var ${ARGN})
    if(NOT ${dep_var})
      set(deps_ok FALSE)
      list(APPEND missing_deps "${dep_var}")
    endif()
  endforeach()
  if(deps_ok)
    message(STATUS "Enabling plugin from ${plugin_dir}")
    add_subdirectory(${plugin_dir})
  else()
    message(STATUS "Skipping ${plugin_dir}: missing dependencies: ${missing_deps}")
  endif()
endfunction()

# Camera plugins (sys/)
add_plugin_if(ENABLE_GST_PLUGIN_CAMIMGREPROC    sys/camimgreproc)
add_plugin_if(ENABLE_GST_PLUGIN_CAMREPROC       sys/camreproc)
add_plugin_if(ENABLE_GST_PLUGIN_JPEGENC         sys/jpegenc)
add_plugin_if(ENABLE_GST_PLUGIN_QMMFSRC         sys/qmmfsrc)

# External Software Plugins (ext/)
add_plugin_if(ENABLE_GST_PLUGIN_REDISSINK       ext/redissink)

# Messaging Plugins (gst/)
# gst/msgbroker: requires gstreamer-1.0, gstreamer-base-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MSGBROKER       gst/msgbroker
  GST_FOUND GST_BASE_FOUND)

# ML Plugins (gst/ and ext/)
# gst/metamux: requires gstreamer-1.0, gstreamer-base-1.0, gstreamer-video-1.0,
#              gstreamer-audio-1.0, gstreamer-qcom-oss-utils-1.0,
#              gstreamer-qcom-oss-video-1.0, gstreamer-qcom-oss-cv-1.0
add_plugin_if(ENABLE_GST_PLUGIN_METAMUX         gst/metamux
  GST_FOUND GST_BASE_FOUND GST_VIDEO_FOUND GST_AUDIO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_CV_FOUND)

# gst/metatransform: requires gstreamer-1.0, gstreamer-base-1.0,
#                    gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0
add_plugin_if(ENABLE_GST_PLUGIN_METATRANSFORM   gst/metatransform
  GST_FOUND GST_BASE_FOUND GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND)

add_plugin_if(ENABLE_GST_PLUGIN_MLACONVERTER    ext/mlaconverter)

# gst/mldemux: requires gstreamer-1.0, gstreamer-base-1.0,
#              gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-ml-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MLDEMUX         gst/mldemux
  GST_FOUND GST_BASE_FOUND GST_QCOM_UTILS_FOUND GST_QCOM_ML_FOUND)

# gst/mlmetaextractor: requires gstreamer-1.0, gstreamer-base-1.0,
#                      gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#                      gstreamer-qcom-oss-video-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MLMETAEXTRACTOR gst/mlmetaextractor
  GST_FOUND GST_BASE_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND)

# gst/mlmetaparser: requires gstreamer-1.0, gstreamer-base-1.0,
#                   gstreamer-allocators-1.0, gstreamer-video-1.0,
#                   gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MLMETAPARSER    gst/mlmetaparser
  GST_FOUND GST_BASE_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND)

# gst/mlpostprocess: requires gstreamer-1.0, gstreamer-base-1.0,
#                    gstreamer-allocators-1.0, gstreamer-video-1.0, cairo,
#                    gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0,
#                    gstreamer-qcom-oss-allocators-1.0, gstreamer-qcom-oss-ml-1.0,
#                    gstreamer-qcom-oss-memory-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MLPOSTPROCESS   gst/mlpostprocess
  GST_FOUND GST_BASE_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND CAIRO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND
  GST_QCOM_ML_FOUND GST_QCOM_MEM_FOUND)

add_plugin_if(ENABLE_GST_PLUGIN_MLQNN           ext/mlqnn)
add_plugin_if(ENABLE_GST_PLUGIN_MLSNPE          ext/mlsnpe)
add_plugin_if(ENABLE_GST_PLUGIN_MLTFLITE        ext/mltflite)
add_plugin_if(ENABLE_GST_PLUGIN_MLONNX          ext/mlonnx)
add_plugin_if(ENABLE_GST_PLUGIN_MLTOOLS         tools/mltools)

# gst/mlvconverter: requires gstreamer-1.0, gstreamer-base-1.0,
#                   gstreamer-allocators-1.0, gstreamer-video-1.0,
#                   gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0,
#                   gstreamer-qcom-oss-allocators-1.0, gstreamer-qcom-oss-ml-1.0
add_plugin_if(ENABLE_GST_PLUGIN_MLVCONVERTER    gst/mlvconverter
  GST_FOUND GST_BASE_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND GST_QCOM_ML_FOUND)

# gst/objtracker: requires gstreamer-1.0, gstreamer-base-1.0,
#                 gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#                 gstreamer-qcom-oss-video-1.0
add_plugin_if(ENABLE_GST_PLUGIN_OBJTRACKER      gst/objtracker
  GST_FOUND GST_BASE_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND)

add_plugin_if(ENABLE_GST_PLUGIN_RESTRICTED_ZONE ext/restricted-zone)

# Video Processing plugins (gst/)
# gst/vcomposer: requires gstreamer-1.0, gstreamer-allocators-1.0,
#                gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#                gstreamer-qcom-oss-video-1.0, gstreamer-qcom-oss-allocators-1.0
add_plugin_if(ENABLE_GST_PLUGIN_VCOMPOSER       gst/vcomposer
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND)

# gst/voverlay: requires gstreamer-1.0, gstreamer-base-1.0,
#               gstreamer-allocators-1.0, gstreamer-video-1.0, cairo,
#               gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0,
#               gstreamer-qcom-oss-allocators-1.0, gstreamer-qcom-oss-cv-1.0
add_plugin_if(ENABLE_GST_PLUGIN_VOVERLAY        gst/voverlay
  GST_FOUND GST_BASE_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND CAIRO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND GST_QCOM_CV_FOUND)

# gst/vsplit: requires gstreamer-1.0, gstreamer-base-1.0,
#             gstreamer-video-1.0, gstreamer-allocators-1.0,
#             gstreamer-qcom-oss-utils-1.0, gstreamer-qcom-oss-video-1.0,
#             gstreamer-qcom-oss-allocators-1.0
add_plugin_if(ENABLE_GST_PLUGIN_VSPLIT          gst/vsplit
  GST_FOUND GST_BASE_FOUND GST_VIDEO_FOUND GST_ALLOC_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND)

# gst/vtransform: requires gstreamer-1.0, gstreamer-allocators-1.0,
#                 gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#                 gstreamer-qcom-oss-video-1.0, gstreamer-qcom-oss-allocators-1.0
add_plugin_if(ENABLE_GST_PLUGIN_VTRANSFORM      gst/vtransform
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_ALLOC_FOUND)

# Software Plugins (gst/ and sys/)
# gst/batch: requires gstreamer-1.0, gstreamer-base-1.0, gstreamer-video-1.0,
#            gstreamer-audio-1.0, gstreamer-qcom-oss-utils-1.0
add_plugin_if(ENABLE_GST_PLUGIN_BATCH           gst/batch
  GST_FOUND GST_BASE_FOUND GST_VIDEO_FOUND GST_AUDIO_FOUND GST_QCOM_UTILS_FOUND)

# gst/rtspbin: requires gstreamer-1.0, gstreamer-allocators-1.0,
#              gstreamer-video-1.0, gstreamer-rtsp-server-1.0
add_plugin_if(ENABLE_GST_PLUGIN_RTSPBIN         gst/rtspbin
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND GST_RTSP_FOUND)

add_plugin_if(ENABLE_GST_PLUGIN_SMARTVENCBIN    sys/smartvencbin)

# gst/socket: requires gstreamer-1.0, gstreamer-allocators-1.0,
#             gstreamer-video-1.0, gstreamer-qcom-oss-video-1.0,
#             gstreamer-qcom-oss-ml-1.0
add_plugin_if(ENABLE_GST_PLUGIN_SOCKET          gst/socket
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_VIDEO_FOUND GST_QCOM_ML_FOUND)

# gst/videotemplate: requires gstreamer-1.0, gstreamer-allocators-1.0,
#                    gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#                    gstreamer-qcom-oss-video-1.0
add_plugin_if(ENABLE_GST_PLUGIN_VIDEOTEMPLATE   gst/videotemplate
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND)

# Sample Apps and Test Framework
add_plugin_if(ENABLE_GST_PLUGIN_EXAMPLES        examples/plugin-examples)
add_plugin_if(ENABLE_GST_PYTHON_EXAMPLES        examples/python)
add_plugin_if(ENABLE_GST_SAMPLE_APPS            examples/sample-apps)
add_plugin_if(ENABLE_GST_SAMPLE_APPS            examples/sample-apps/gst-sample-apps-utils)
add_plugin_if(ENABLE_GST_PLUGIN_TOOLS           tools/gst-plugin-tools)
add_plugin_if(ENABLE_GST_TEST_FRAMEWORK         tests/test-framework)
add_plugin_if(ENABLE_GST_UMD_DAEMON             sys/umd-daemon)

# Old ML Plugins (ext/)
add_plugin_if(ENABLE_GST_PLUGIN_MLVDETECTION        ext/mlvdetection)
add_plugin_if(ENABLE_GST_PLUGIN_MLVPOSE             ext/mlvpose)
add_plugin_if(ENABLE_GST_PLUGIN_MLVSEGMENTATION     ext/mlvsegmentation)
add_plugin_if(ENABLE_GST_PLUGIN_MLVSUPERRESOLUTION  ext/mlvsuperresolution)

# ACK SP Plugins (sys/ and ext/)
add_plugin_if(ENABLE_GST_PLUGIN_DFS             sys/dfs)
add_plugin_if(ENABLE_GST_PLUGIN_DNGPACKER       sys/dngpacker)
add_plugin_if(ENABLE_GST_PLUGIN_HEIFMUX         ext/heifmux)
add_plugin_if(ENABLE_GST_PLUGIN_HEXAGON         sys/hexagon)
add_plugin_if(ENABLE_GST_PLUGIN_JPEGPACKER      sys/jpegpacker)
add_plugin_if(ENABLE_GST_PLUGIN_MLAIC           ext/mlaic)

# gst/overlay: requires gstreamer-1.0, gstreamer-allocators-1.0,
#              gstreamer-video-1.0, gstreamer-qcom-oss-utils-1.0,
#              gstreamer-qcom-oss-video-1.0, gstreamer-qcom-oss-cv-1.0
add_plugin_if(ENABLE_GST_PLUGIN_OVERLAY         gst/overlay
  GST_FOUND GST_ALLOC_FOUND GST_VIDEO_FOUND
  GST_QCOM_UTILS_FOUND GST_QCOM_VIDEO_FOUND GST_QCOM_CV_FOUND)
