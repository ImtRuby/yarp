# Copyright (C) 2006-2018 Istituto Italiano di Tecnologia (IIT)
# All rights reserved.
#
# This software may be modified and distributed under the terms of the
# BSD-3-Clause license. See the accompanying LICENSE file for details.

yarp_prepare_plugin(transformServer
                    CATEGORY device
                    TYPE yarp::dev::FrameTransformServer
                    INCLUDE FrameTransformServer.h
                    DEPENDS "YARP_HAS_MATH_LIB"
                    DEFAULT ON)

if(NOT SKIP_transformServer)
  set(CMAKE_INCLUDE_CURRENT_DIR ON)

  yarp_add_plugin(yarp_transformServer FrameTransformServer.cpp
                                       FrameTransformServer.h)
  target_link_libraries(yarp_transformServer PRIVATE YARP::YARP_OS
                                                     YARP::YARP_sig
                                                     YARP::YARP_dev
                                                     YARP::YARP_math
                                                     YARP::YARP_rosmsg)
  list(APPEND YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS YARP_OS
                                                      YARP_sig
                                                      YARP_dev
                                                      YARP_math
                                                      YARP_rosmsg)

  yarp_install(TARGETS yarp_transformServer
               EXPORT YARP_${YARP_PLUGIN_MASTER}
               COMPONENT ${YARP_PLUGIN_MASTER}
               LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
               ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR})
  yarp_install(FILES transformServer.ini
               COMPONENT ${YARP_PLUGIN_MASTER}
               DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR})

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_transformServer PROPERTY FOLDER "Plugins/Device")
endif()
