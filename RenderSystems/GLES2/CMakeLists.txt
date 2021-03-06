#-------------------------------------------------------------------
# This file is part of the CMake build system for OGRE
#     (Object-oriented Graphics Rendering Engine)
# For the latest info, see http://www.ogre3d.org/
#
# The contents of this file are placed in the public domain. Feel
# free to make use of it in any way you like.
#-------------------------------------------------------------------

# Configure OpenGL ES 2.0 RenderSystem build

set(HEADER_FILES
  include/OgreGLES2Context.h
  include/OgreGLES2DefaultHardwareBufferManager.h
  include/OgreGLES2DepthBuffer.h
  include/OgreGLES2FBOMultiRenderTarget.h
  include/OgreGLES2FBORenderTexture.h
  include/OgreGLES2FrameBufferObject.h
  include/OgreGLES2GpuProgram.h
  include/OgreGLES2GpuProgramManager.h
  include/OgreGLES2HardwareBufferManager.h
  include/OgreGLES2HardwareIndexBuffer.h
  include/OgreGLES2HardwareOcclusionQuery.h
  include/OgreGLES2HardwarePixelBuffer.h
  include/OgreGLES2HardwareUniformBuffer.h
  include/OgreGLES2HardwareVertexBuffer.h
  include/OgreGLES2PixelFormat.h
  include/OgreGLES2Plugin.h
  include/OgreGLES2Prerequisites.h
  include/OgreGLES2RenderSystem.h
  include/OgreGLES2RenderTexture.h
  include/OgreGLES2RenderToVertexBuffer.h
  include/OgreGLES2StateCacheManager.h
  include/OgreGLES2Support.h
  include/OgreGLES2Texture.h
  include/OgreGLES2TextureManager.h
  include/OgreGLES2UniformCache.h
  include/OgreGLES2VertexDeclaration.h
)

set(SOURCE_FILES
  src/OgreGLES2Context.cpp
  src/OgreGLES2DefaultHardwareBufferManager.cpp
  src/OgreGLES2DepthBuffer.cpp
  src/OgreGLES2EngineDll.cpp
  src/OgreGLES2FBOMultiRenderTarget.cpp
  src/OgreGLES2FBORenderTexture.cpp
  src/OgreGLES2FrameBufferObject.cpp
  src/OgreGLES2GpuProgram.cpp
  src/OgreGLES2GpuProgramManager.cpp
  src/OgreGLES2HardwareBufferManager.cpp
  src/OgreGLES2HardwareIndexBuffer.cpp
  src/OgreGLES2HardwareOcclusionQuery.cpp
  src/OgreGLES2HardwarePixelBuffer.cpp
  src/OgreGLES2HardwareUniformBuffer.cpp
  src/OgreGLES2HardwareVertexBuffer.cpp
  src/OgreGLES2PixelFormat.cpp
  src/OgreGLES2Plugin.cpp
  src/OgreGLES2RenderSystem.cpp
  src/OgreGLES2RenderTexture.cpp
  src/OgreGLES2RenderToVertexBuffer.cpp
  src/OgreGLES2StateCacheManager.cpp
  src/OgreGLES2Support.cpp
  src/OgreGLES2Texture.cpp
  src/OgreGLES2TextureManager.cpp
  src/OgreGLES2UniformCache.cpp
  src/OgreGLES2VertexDeclaration.cpp
)

include_directories(src/StateCacheManager)
if(OGRE_CONFIG_ENABLE_GLES2_STATE_CACHE_SUPPORT)
  set(HEADER_FILES
      ${HEADER_FILES}
      src/StateCacheManager/OgreGLES2StateCacheManagerImp.h
      src/StateCacheManager/OgreGLES2UniformCacheImp.h
  )
  set(SOURCE_FILES
      ${SOURCE_FILES}
      src/StateCacheManager/OgreGLES2StateCacheManagerImp.cpp
      src/StateCacheManager/OgreGLES2UniformCacheImp.cpp
  )
else()
  set(HEADER_FILES
      ${HEADER_FILES}
      src/StateCacheManager/OgreGLES2NullStateCacheManagerImp.h
      src/StateCacheManager/OgreGLES2NullUniformCacheImp.h
  )
  set(SOURCE_FILES
      ${SOURCE_FILES}
      src/StateCacheManager/OgreGLES2NullStateCacheManagerImp.cpp
      src/StateCacheManager/OgreGLES2NullUniformCacheImp.cpp
  )
endif()

set(GLSLES_FILES
  src/GLSLES/include/OgreGLSLESExtSupport.h
  src/GLSLES/include/OgreGLSLESGpuProgram.h
  src/GLSLES/include/OgreGLSLESLinkProgram.h
  src/GLSLES/include/OgreGLSLESLinkProgramManager.h
  src/GLSLES/include/OgreGLSLESPreprocessor.h
  src/GLSLES/include/OgreGLSLESProgram.h
  src/GLSLES/include/OgreGLSLESProgramCommon.h
  src/GLSLES/include/OgreGLSLESProgramFactory.h
  src/GLSLES/include/OgreGLSLESProgramManagerCommon.h
  src/GLSLES/include/OgreGLSLESProgramPipeline.h
  src/GLSLES/include/OgreGLSLESProgramPipelineManager.h
  src/GLSLES/src/OgreGLSLESExtSupport.cpp
  src/GLSLES/src/OgreGLSLESGpuProgram.cpp
  src/GLSLES/src/OgreGLSLESLinkProgram.cpp
  src/GLSLES/src/OgreGLSLESLinkProgramManager.cpp
  src/GLSLES/src/OgreGLSLESPreprocessor.cpp
  src/GLSLES/src/OgreGLSLESProgram.cpp
  src/GLSLES/src/OgreGLSLESProgramCommon.cpp
  src/GLSLES/src/OgreGLSLESProgramFactory.cpp
  src/GLSLES/src/OgreGLSLESProgramManagerCommon.cpp
  src/GLSLES/src/OgreGLSLESProgramPipeline.cpp
  src/GLSLES/src/OgreGLSLESProgramPipelineManager.cpp
)

if (OGRE_CONFIG_ENABLE_GLES2_CG_SUPPORT)
  set(GLSLES_FILES
    src/GLSLES/src/OgreGLSLESCgProgram.cpp
    src/GLSLES/src/OgreGLSLESCgProgramFactory.cpp
    ${GLSLES_FILES}
  )
endif (OGRE_CONFIG_ENABLE_GLES2_CG_SUPPORT)

if(NOT OPENGLES3_FOUND)
  set(OPENGLES3_INCLUDE_DIR "")
endif()

# Add system specific settings
if (OGRE_BUILD_PLATFORM_NACL)
  set(PLATFORM_HEADERS
    include/NaCl/OgreGLES2Util.h
    include/NaCl/OgreNaClGLContext.h
    include/NaCl/OgreNaClGLSupport.h
    include/NaCl/OgreNaClWindow.h
  )
  set(PLATFORM_SOURCES
    src/NaCl/OgreNaClGLContext.cpp
    src/NaCl/OgreNaClGLSupport.cpp
    src/NaCl/OgreNaClWindow.cpp
  )
  include_directories(src/NaCl include/NaCl)
  set(PLATFORM_HEADER_INSTALL "NaCl")
elseif (WIN32)
  set(PLATFORM_HEADERS
    include/EGL/WIN32/OgreWin32EGLContext.h
    include/EGL/WIN32/OgreWin32EGLSupport.h
    include/EGL/WIN32/OgreWin32EGLRenderTexture.h
    include/EGL/WIN32/OgreWin32EGLWindow.h
    include/EGL/WIN32/OgreGLES2Util.h
    include/EGL/OgreEGLContext.h
    include/EGL/OgreEGLRenderTexture.h
    include/EGL/OgreEGLSupport.h
    include/EGL/OgreEGLWindow.h
  )
  set(PLATFORM_SOURCES
    src/EGL/WIN32/OgreWin32EGLSupport.cpp
    src/EGL/WIN32/OgreWin32EGLRenderTexture.cpp
    src/EGL/WIN32/OgreWin32EGLWindow.cpp
    src/EGL/WIN32/OgreWin32EGLContext.cpp
    src/EGL/OgreEGLContext.cpp
    src/EGL/OgreEGLRenderTexture.cpp
    src/EGL/OgreEGLSupport.cpp
    src/EGL/OgreEGLWindow.cpp
  )
  include_directories(src/EGL/WIN32 include/EGL/WIN32)
  if(OGRE_CONFIG_ENABLE_GLES3_SUPPORT)
    link_directories(${OPENGLES3_LIBRARY_PATH})
  else()
    link_directories(${OPENGLES2_LIBRARY_PATH})
  endif()
  set(PLATFORM_HEADER_INSTALL "WIN32")
elseif (ANDROID)
  set(PLATFORM_HEADERS
    include/EGL/Android/OgreAndroidEGLContext.h
    include/EGL/Android/OgreAndroidEGLSupport.h
    include/EGL/Android/OgreAndroidEGLWindow.h
    include/EGL/Android/OgreGLES2Util.h
    include/EGL/Android/OgreAndroidResourceManager.h
    include/EGL/Android/OgreAndroidResource.h
    include/EGL/OgreEGLContext.h
    include/EGL/OgreEGLRenderTexture.h
    include/EGL/OgreEGLSupport.h
    include/EGL/OgreEGLWindow.h
  )
  set(PLATFORM_SOURCES
    src/EGL/Android/OgreAndroidEGLContext.cpp
    src/EGL/Android/OgreAndroidEGLSupport.cpp
    src/EGL/Android/OgreAndroidEGLWindow.cpp
    src/EGL/Android/OgreAndroidResourceManager.cpp
    src/EGL/Android/OgreAndroidResource.cpp
    src/EGL/OgreEGLContext.cpp
    src/EGL/OgreEGLRenderTexture.cpp
    src/EGL/OgreEGLSupport.cpp
    src/EGL/OgreEGLWindow.cpp
  )

  include_directories(src/EGL/Android include/EGL/Android)
  if(OGRE_CONFIG_ENABLE_GLES3_SUPPORT)
    link_directories(${OPENGLES3_LIBRARY_PATH})
  else()
    link_directories(${OPENGLES2_LIBRARY_PATH})
  endif()
  set(PLATFORM_HEADER_INSTALL "ANDROID")
elseif (APPLE)
  set(PLATFORM_HEADERS
    include/EAGL/OgreEAGLES2Context.h
    include/EAGL/OgreEAGL2Support.h
    include/EAGL/OgreEAGL2View.h
    include/EAGL/OgreEAGL2ViewController.h
    include/EAGL/OgreEAGL2Window.h
    include/EAGL/OgreGLES2Util.h
  )
  set(PLATFORM_SOURCES
    src/EAGL/OgreEAGL2Support.mm
    src/EAGL/OgreEAGL2View.mm
    src/EAGL/OgreEAGL2ViewController.mm
    src/EAGL/OgreEAGL2Window.mm
    src/EAGL/OgreEAGLES2Context.mm
  )
  include_directories(src/EAGL include/EAGL)
  link_directories(${OPENGLES2_LIBRARY_PATH})
  set(PLATFORM_HEADER_INSTALL "APPLE")
elseif (UNIX)
  set(PLATFORM_HEADERS
    include/EGL/X11/OgreX11EGLContext.h
    include/EGL/X11/OgreX11EGLSupport.h
    include/EGL/X11/OgreX11EGLRenderTexture.h
    include/EGL/X11/OgreX11EGLWindow.h
    include/EGL/X11/OgreGLES2Util.h
    include/EGL/OgreEGLContext.h
    include/EGL/OgreEGLRenderTexture.h
    include/EGL/OgreEGLSupport.h
    include/EGL/OgreEGLWindow.h
  )
  set(PLATFORM_SOURCES
    src/EGL/X11/OgreX11EGLContext.cpp
    src/EGL/X11/OgreX11EGLSupport.cpp
    src/EGL/X11/OgreX11EGLRenderTexture.cpp
    src/EGL/X11/OgreX11EGLWindow.cpp
    src/EGL/OgreEGLContext.cpp
    src/EGL/OgreEGLRenderTexture.cpp
    src/EGL/OgreEGLSupport.cpp
    src/EGL/OgreEGLWindow.cpp
  )
  include_directories(src/EGL/X11 include/EGL/X11)
  set(PLATFORM_HEADER_INSTALL "X11")
  set(PLATFORM_LIBS ${X11_LIBRARIES} ${X11_Xrandr_LIB})
endif ()

# Add support for the RT Shader System
add_definitions(-DUSE_RTSHADER_SYSTEM)

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${CMAKE_CURRENT_SOURCE_DIR}/include/EGL
  ${CMAKE_CURRENT_SOURCE_DIR}/include/EAGL
  ${CMAKE_CURRENT_SOURCE_DIR}/src/GLSLES/include
  ${CMAKE_SOURCE_DIR}/Components/RTShaderSystem/include
  ${OPENGLES3_INCLUDE_DIR} ${OPENGLES2_INCLUDE_DIR} ${EGL_INCLUDE_DIR}
)

ogre_add_library(RenderSystem_GLES2 ${OGRE_LIB_TYPE} ${HEADER_FILES} ${SOURCE_FILES} ${GLSLES_FILES} ${PLATFORM_HEADERS} ${PLATFORM_SOURCES})
target_link_libraries(RenderSystem_GLES2 OgreMain ${OPENGLES3_LIBRARIES} ${OPENGLES2_LIBRARIES} ${EGL_LIBRARIES} ${PLATFORM_LIBS})

if (NOT OGRE_STATIC)
  set_target_properties(RenderSystem_GLES2 PROPERTIES
    COMPILE_DEFINITIONS OGRE_GLES2PLUGIN_EXPORTS
  )
endif ()

if (OGRE_CONFIG_THREADS)
  target_link_libraries(RenderSystem_GLES2 ${OGRE_THREAD_LIBRARIES})
endif ()

ogre_config_plugin(RenderSystem_GLES2)
install(FILES ${HEADER_FILES} DESTINATION include/OGRE/RenderSystems/GLES2)
install(FILES ${PLATFORM_HEADERS} DESTINATION include/OGRE/RenderSystems/GLES2/${PLATFORM_HEADER_INSTALL})
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/src/GLSLES/include/ DESTINATION include/OGRE/RenderSystems/GLES2/${PLATFORM_HEADER_INSTALL})
