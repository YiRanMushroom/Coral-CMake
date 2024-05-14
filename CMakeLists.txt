cmake_minimum_required(VERSION 3.19)

set(CMAKE_CXX_STANDARD 20)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE BOOL "" FORCE)

if(NOT CMAKE_DOTNET_SDK)
  set(CMAKE_DOTNET_SDK "Microsoft.NET.Sdk")
endif()

if(NOT CORAL_DOTNET_VERSION)
  set(CORAL_DOTNET_VERSION "net8.0")
endif()

if(NOT CORAL_CSHARP_FLAGS)
  set(CORAL_CSHARP_FLAGS "/langversion:12")
endif()

set(CMAKE_DOTNET_TARGET_FRAMEWORK ${CORAL_DOTNET_VERSION})
set(CMAKE_CSharp_FLAGS ${CORAL_CSHARP_FLAGS})
set(CMAKE_VS_NUGET_PACKAGE_RESTORE ON)

project(Coral
        VERSION 1.0.0
        DESCRIPTION "C++/C# wrapper around the .NET CoreCLR library, the purpose of Coral is to provide a native interface similar to Mono, but in a more modern style, and using .NET Core instead of .NET Framework "
        HOMEPAGE_URL "https://github.com/StudioCherno/Coral"
        LANGUAGES CXX C CSharp
)

option(CORAL_BUILD_TESTS "Build the tests" OFF)
option(CORAL_BUILD_EXAMPLES "Build the tests" OFF)

add_subdirectory(Coral.Native)
add_subdirectory(Coral.Managed)

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