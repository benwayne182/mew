cmake_minimum_required(VERSION 2.8)
include_directories(/opt/grx/include/OpenHRP-3.1)
link_directories(/opt/grx/lib)
set(libname ergocycleCustomizer)

set(sources customizer.cpp)

add_library(${libname} SHARED ${sources})

if(UNIX)
  target_link_libraries(
    ${libname}
     hrpModel-3.1)#${OPENHRP_LIBRARY_VERSION})
elseif(WIN32)
  set_target_properties(${libname} PROPERTIES DEBUG_POSTFIX d )
  target_link_libraries(${libname}
    optimized hrpModel-${OPENHRP_LIBRARY_VERSION}
    debug hrpModel-${OPENHRP_LIBRARY_VERSION}d
    )
endif()

install(TARGETS ${libname} DESTINATION ${RELATIVE_SHARE_INSTALL_PATH}/customizer CONFIGURATIONS Release Debug)
