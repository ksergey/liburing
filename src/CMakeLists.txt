set(sources queue.c register.c setup.c syscall.c syscall.h)

add_library(uring)
target_compile_options(uring
  PRIVATE -Wall -Wextra)
target_include_directories(uring
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

foreach(file ${sources})
  target_sources(uring PRIVATE ${file})
endforeach()

install(TARGETS uring
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)

install(FILES include/liburing.h DESTINATION include)
install(FILES include/liburing/barrier.h DESTINATION include/liburing)
install(FILES include/liburing/io_uring.h DESTINATION include/liburing)
