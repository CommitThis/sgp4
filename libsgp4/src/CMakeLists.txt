set(SRCS
    CoordGeodetic.cc
    CoordTopocentric.cc
    DateTime.cc
    DecayedException.cc
    Eci.cc
    Globals.cc
    Observer.cc
    OrbitalElements.cc
    SGP4.cc
    SatelliteException.cc
    SolarPosition.cc
    TimeSpan.cc
    Tle.cc
    TleException.cc
    Util.cc
    Vector.cc)

set(INCS
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/CoordGeodetic.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/CoordTopocentric.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/DateTime.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/DecayedException.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Eci.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Globals.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Observer.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/OrbitalElements.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/SatelliteException.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/SGP4.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/SolarPosition.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/TimeSpan.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/TleException.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Tle.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Util.h
     ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4/Vector.h
     )


include(GNUInstallDirs)


add_library(sgp4 STATIC ${SRCS})
add_Library(sgp4::sgp4-static ALIAS sgp4)
target_include_directories(sgp4 
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/>
        $<INSTALL_INTERFACE:include>
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4
)

set_target_properties(sgp4 PROPERTIES PUBLIC_HEADER "${INCS}")
install(TARGETS sgp4
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} 
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/sgp4)


add_library(sgp4s SHARED ${SRCS})
add_Library(sgp4::sgp4 ALIAS sgp4s)
target_include_directories(sgp4s 
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/>
        $<INSTALL_INTERFACE:include>
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/../include/sgp4
)
set_target_properties(sgp4s PROPERTIES PUBLIC_HEADER "${INCS}")

# Don't install headers with shared library
install( TARGETS sgp4s 
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

