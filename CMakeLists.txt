cmake_minimum_required(VERSION 3.19)

set(CMAKE_CXX_STANDARD 20)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE BOOL "" FORCE)

project(Coral
  VERSION 1.0.0
  DESCRIPTION "C++/C# wrapper around the .NET CoreCLR library, the purpose of Coral is to provide a native interface similar to Mono, but in a more modern style, and using .NET Core instead of .NET Framework "
  HOMEPAGE_URL "https://github.com/StudioCherno/Coral"
)

option(CORAL_BUILD_NATIVE   "Builds the Native Coral library" ON)
option(CORAL_BUILD_MANAGED  "Builds the Managed Coral library" OFF)
option(CORAL_BUILD_TESTS    "Build the tests" OFF)
option(CORAL_BUILD_TESTS    "Build the tests" OFF)
option(CORAL_BUILD_EXAMPLES "Build the tests" OFF)

# Override for custom CXX_FLAGS
# Note: If passing a string with flags, make sure to separate every flag with a semicolon ;
if(NOT CORAL_NATIVE_MSVC_FLAGS)
#  set(CORAL_NATIVE_MSVC_FLAGS "/WX")
endif()

if(CORAL_BUILD_NATIVE)
  add_subdirectory(Coral.Native)
endif()

if(CORAL_BUILD_MANAGED)
add_subdirectory(Coral.Managed)
endif()

if(CORAL_BUILD_TESTS)
#    TODO
#    add_subdirectory(Tests/Testing.Native)
#    add_subdirectory(Tests/Testing.Managed)
endif()

if(CORAL_BUILD_EXAMPLES)
#    TODO
#    add_subdirectory(Example/Example.Native)
#    add_subdirectory(Example/Example.Managed)
endif()