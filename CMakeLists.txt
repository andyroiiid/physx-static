cmake_minimum_required(VERSION 3.2)
project(PhysX CXX)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(PHYSX_TYPE debug)
else ()
    set(PHYSX_TYPE release)
endif ()

add_library(PhysX::PhysXExtensions STATIC IMPORTED)
set_target_properties(PhysX::PhysXExtensions PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXExtensions_static_64.lib)

add_library(PhysX::PhysX STATIC IMPORTED)
set_target_properties(PhysX::PhysX PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysX_static_64.lib)

add_library(PhysX::PhysXPvdSDK STATIC IMPORTED)
set_target_properties(PhysX::PhysXPvdSDK PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXPvdSDK_static_64.lib)

add_library(PhysX::PhysXVehicle STATIC IMPORTED)
set_target_properties(PhysX::PhysXVehicle PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXVehicle_static_64.lib)

add_library(PhysX::PhysXCharacterKinematic STATIC IMPORTED)
set_target_properties(PhysX::PhysXCharacterKinematic PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXCharacterKinematic_static_64.lib)

add_library(PhysX::PhysXCooking STATIC IMPORTED)
set_target_properties(PhysX::PhysXCooking PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXCooking_static_64.lib)

add_library(PhysX::PhysXCommon STATIC IMPORTED)
set_target_properties(PhysX::PhysXCommon PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXCommon_static_64.lib)

add_library(PhysX::PhysXFoundation STATIC IMPORTED)
set_target_properties(PhysX::PhysXFoundation PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/PhysXFoundation_static_64.lib)

add_library(PhysX INTERFACE IMPORTED GLOBAL)

target_include_directories(PhysX INTERFACE include)

target_compile_definitions(PhysX INTERFACE PX_PHYSX_STATIC_LIB)

target_link_libraries(PhysX INTERFACE
        PhysX::PhysXExtensions
        PhysX::PhysX
        PhysX::PhysXPvdSDK
        PhysX::PhysXVehicle
        PhysX::PhysXCharacterKinematic
        PhysX::PhysXCooking
        PhysX::PhysXCommon
        PhysX::PhysXFoundation)
