CONTENT="cmake_minimum_required(VERSION 3.5.1)
project(tensorflow VERSION 2.4.0)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add TensorFlow source files
add_subdirectory(tensorflow/core)
add_subdirectory(tensorflow/compiler)
add_subdirectory(tensorflow/python)

# Add TensorFlow libraries
target_link_libraries(tensorflow
  tensorflow::core
  tensorflow::compiler
  tensorflow::python
  ${TENSORFLOW_EXTERNAL_LIBS}
)

# Add TensorFlow include directories
target_include_directories(tensorflow
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/tensorflow>
    $<INSTALL_INTERFACE:include>
)

# Set TensorFlow installation options
install(TARGETS tensorflow
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib/static
)

install(DIRECTORY include/ DESTINATION include)"
