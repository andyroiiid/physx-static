cmake_minimum_required(VERSION 3.2)
project(PhysX CXX)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(PHYSX_TYPE debug)
else ()
    set(PHYSX_TYPE checked)
endif ()

macro(physx_module module)
    add_library(PhysX::${module} STATIC IMPORTED)
    set_target_properties(PhysX::${module} PROPERTIES
            IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/lib/${PHYSX_TYPE}/${module}_static_64.lib)
endmacro()

physx_module(PhysX)
physx_module(PhysXCharacterKinematic)
physx_module(PhysXCommon)
physx_module(PhysXCooking)
physx_module(PhysXExtensions)
physx_module(PhysXFoundation)
physx_module(PhysXPvdSDK)
physx_module(PhysXVehicle)
physx_module(PhysXVehicle2)

add_library(PhysX INTERFACE IMPORTED GLOBAL)

target_include_directories(PhysX INTERFACE include)

target_compile_definitions(PhysX INTERFACE PX_PHYSX_STATIC_LIB)

target_link_libraries(PhysX INTERFACE
        PhysX::PhysX
        PhysX::PhysXCharacterKinematic
        PhysX::PhysXCommon
        PhysX::PhysXCooking
        PhysX::PhysXExtensions
        PhysX::PhysXFoundation
        PhysX::PhysXPvdSDK
        PhysX::PhysXVehicle
        PhysX::PhysXVehicle2)