# When debugging the timezone widget, add this debugging definition
# to have a debugging-friendly timezone widget, debug logging,
# and no intrusive timezone-setting while clicking around.
option( DEBUG_TIMEZONES "Debug-friendly timezone widget." OFF )
if( DEBUG_TIMEZONES )
    add_definitions( -DDEBUG_TIMEZONES )
endif()

find_package(Qt5Location CONFIG)
set_package_properties(Qt5Location PROPERTIES
    DESCRIPTION "Used for rendering the map"
    TYPE RUNTIME
)
find_package(Qt5Positioning CONFIG)
set_package_properties(Qt5Positioning PROPERTIES
    DESCRIPTION "Used for GeoLocation and GeoCoding"
    TYPE RUNTIME
)

# Because we're sharing sources with the regular locale module
set( _locale ${CMAKE_CURRENT_SOURCE_DIR}/../locale )

include_directories( ${_locale} )

calamares_add_plugin( localeq
    TYPE viewmodule
    EXPORT_MACRO PLUGINDLLEXPORT_PRO
    SOURCES
        LocaleQmlViewStep.cpp
        ${_locale}/LocaleConfiguration.cpp
        ${_locale}/Config.cpp
        ${_locale}/SetTimezoneJob.cpp
    RESOURCES
        localeq.qrc
    LINK_PRIVATE_LIBRARIES
        calamaresui
        Qt5::Network
    SHARED_LIB
)
