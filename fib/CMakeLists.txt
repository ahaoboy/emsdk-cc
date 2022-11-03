project(fib LANGUAGES C)

set(fib_src fib.cc)
add_library(fib ${fib_src})
