if(NOT DEFINED NSX_BOARD_FLAGS_TARGET)
    message(FATAL_ERROR "Board must define NSX_BOARD_FLAGS_TARGET before ns-harness is added.")
endif()

set(nsx_harness_sources
    ${CMAKE_CURRENT_LIST_DIR}/src/ns-ambiqsuite-harness.c
)

add_library(nsx_harness STATIC ${nsx_harness_sources})
set_target_properties(nsx_harness PROPERTIES EXPORT_NAME harness)
add_library(nsx::harness ALIAS nsx_harness)

target_link_libraries(nsx_harness PUBLIC ${NSX_BOARD_FLAGS_TARGET} nsx_soc_hal nsx_core)

target_include_directories(nsx_harness PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/includes-api>
    $<BUILD_INTERFACE:${NSX_ROOT}/modules/nsx-core/includes-api>
    $<BUILD_INTERFACE:${NSX_ROOT}/modules/nsx-utils/includes-api>
    $<BUILD_INTERFACE:${NSX_ROOT}/modules/nsx-perf/includes-api>
    $<BUILD_INTERFACE:${NSX_ROOT}/modules/nsx-pmu-armv8m/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-harness/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-core/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-utils/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-perf/includes-api>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-pmu-armv8m/includes-api>
)

target_link_libraries(nsx_runtime_core INTERFACE nsx_harness)

install(DIRECTORY
    ${CMAKE_CURRENT_LIST_DIR}/includes-api
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/nsx/modules/nsx-harness
)

install(TARGETS
    nsx_harness
    EXPORT nsxTargets
)
