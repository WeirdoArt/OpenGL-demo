cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project (OpenGL-demo)

# src
add_executable(OpenGL-demo "src/Application.cpp")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET OpenGL-demo PROPERTY CXX_STANDARD 17)
endif()

# link
target_include_directories(OpenGL-demo PRIVATE "${CMAKE_SOURCE_DIR}/deps/include")
target_link_directories(OpenGL-demo PRIVATE "${CMAKE_SOURCE_DIR}/deps/lib")
target_link_libraries(OpenGL-demo PRIVATE glew32s glfw3 OpenGL32)
target_compile_definitions(OpenGL-demo PRIVATE GLEW_STATIC)

