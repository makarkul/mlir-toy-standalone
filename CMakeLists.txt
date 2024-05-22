cmake_minimum_required(VERSION 3.22)

project(mlir-toy LANGUAGES CXX C)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
include(MLIRToy)


set(LLVM_LINK_COMPONENTS
  Support
  )

add_llvm_example(toyc
  toyc.cpp
  parser/AST.cpp
  )

include_directories(include)
target_link_libraries(toyc
  PRIVATE
    MLIRSupport
  )
