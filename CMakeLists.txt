cmake_minimum_required(VERSION 3.8)
project(main)
set(CMAKE_BUILD_TYPE DEBUG)

set(CMAKE_CXX_STANDARD 17)

if(CMAKE_COMPILER_IS_GNUCC)
    add_compile_options(-Wall -Wno-unused-parameter)
endif()

add_subdirectory(fib)
add_executable(main main.cc fib/fib.cc)
target_link_libraries(main fib)


set(WASM_FLAG "-O3 -s WASM=1 -s ALLOW_MEMORY_GROWTH ")
if(EMSCRIPTEN)
  message("emcc")
  set(CMAKE_C_COMPILER "emcc")
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${WASM_FLAG}")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${WASM_FLAG}")
  set(WASM_OUTPUT ".html")
  set(CMAKE_EXECUTABLE_SUFFIX "${WASM_OUTPUT}")
endif()

 