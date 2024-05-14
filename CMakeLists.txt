cmake_minimum_required(VERSION 3.19)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

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

project(Coral
        VERSION 1.0.0
        DESCRIPTION "C++/C# wrapper around the .NET CoreCLR library, the purpose of Coral is to provide a native interface similar to Mono, but in a more modern style, and using .NET Core instead of .NET Framework "
        HOMEPAGE_URL "https://github.com/StudioCherno/Coral"
        LANGUAGES CXX C CSharp
)

option(CORAL_BUILD_TESTS "Build the tests" OFF)
option(CORAL_BUILD_EXAMPLES "Build the tests" OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE BOOL "" FORCE)

#add_subdirectory(Coral.Native)
add_subdirectory(Coral.Managed)

if(CORAL_BUILD_TESTS)
    add_subdirectory(Tests/Testing.Native)
    add_subdirectory(Tests/Testing.Managed)
endif()

if(CORAL_BUILD_EXAMPLES)
    add_subdirectory(Example/Example.Native)
    add_subdirectory(Example/Example.Managed)
endif()