
set(microprofile_source
	${CMAKE_CURRENT_SOURCE_DIR}/microprofile.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/microprofile.h
	${CMAKE_CURRENT_SOURCE_DIR}/microprofile_html.h
)

set(CMAKE_POSITION_INDEPENDENT_CODE on)
add_library(microprofile STATIC ${microprofile_source})
set_property(TARGET microprofile PROPERTY CXX_STANDARD 11)
target_compile_definitions(microprofile PRIVATE MICROPROFILE_USE_CONFIG=1)

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  target_compile_options(microprofile
  PRIVATE
    -fvisibility=hidden
  )
endif()

target_include_directories(microprofile PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(microprofile PRIVATE profiler)
