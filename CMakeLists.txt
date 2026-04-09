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

# Helper function to add sub-dir when option set
function(add_plugin_if option_var plugin_dir)
  if(DEFINED ${option_var} AND ${option_var})
    message(STATUS "Enabling plugin from ${plugin_dir}")
    add_subdirectory(${plugin_dir})
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
add_plugin_if(ENABLE_GST_PLUGIN_MSGBROKER       gst/msgbroker)

# ML Plugins (gst/ and ext/)
add_plugin_if(ENABLE_GST_PLUGIN_METAMUX         gst/metamux)
add_plugin_if(ENABLE_GST_PLUGIN_METATRANSFORM   gst/metatransform)
add_plugin_if(ENABLE_GST_PLUGIN_MLACONVERTER    ext/mlaconverter)
add_plugin_if(ENABLE_GST_PLUGIN_MLDEMUX         gst/mldemux)
add_plugin_if(ENABLE_GST_PLUGIN_MLMETAEXTRACTOR gst/mlmetaextractor)
add_plugin_if(ENABLE_GST_PLUGIN_MLMETAPARSER    gst/mlmetaparser)
add_plugin_if(ENABLE_GST_PLUGIN_MLPOSTPROCESS   gst/mlpostprocess)
add_plugin_if(ENABLE_GST_PLUGIN_MLQNN           ext/mlqnn)
add_plugin_if(ENABLE_GST_PLUGIN_MLSNPE          ext/mlsnpe)
add_plugin_if(ENABLE_GST_PLUGIN_MLTFLITE        ext/mltflite)
add_plugin_if(ENABLE_GST_PLUGIN_MLONNX          ext/mlonnx)
add_plugin_if(ENABLE_GST_PLUGIN_MLTOOLS         tools/mltools)
add_plugin_if(ENABLE_GST_PLUGIN_MLVCONVERTER    gst/mlvconverter)
add_plugin_if(ENABLE_GST_PLUGIN_OBJTRACKER      gst/objtracker)
add_plugin_if(ENABLE_GST_PLUGIN_RESTRICTED_ZONE ext/restricted-zone)

# Video Processing plugins (gst/)
add_plugin_if(ENABLE_GST_PLUGIN_VCOMPOSER       gst/vcomposer)
add_plugin_if(ENABLE_GST_PLUGIN_VOVERLAY        gst/voverlay)
add_plugin_if(ENABLE_GST_PLUGIN_VSPLIT          gst/vsplit)
add_plugin_if(ENABLE_GST_PLUGIN_VTRANSFORM      gst/vtransform)

# Software Plugins (gst/ and sys/)
add_plugin_if(ENABLE_GST_PLUGIN_BATCH           gst/batch)
add_plugin_if(ENABLE_GST_PLUGIN_RTSPBIN         gst/rtspbin)
add_plugin_if(ENABLE_GST_PLUGIN_SMARTVENCBIN    sys/smartvencbin)
add_plugin_if(ENABLE_GST_PLUGIN_SOCKET          gst/socket)
add_plugin_if(ENABLE_GST_PLUGIN_VIDEOTEMPLATE   gst/videotemplate)

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
add_plugin_if(ENABLE_GST_PLUGIN_OVERLAY         gst/overlay)
