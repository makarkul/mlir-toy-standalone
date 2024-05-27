cmake_minimum_required(VERSION 3.22)

project(mlir-toy LANGUAGES CXX C)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
include(MLIRToy)

add_subdirectory(include)

set(LLVM_LINK_COMPONENTS
  Support
  )

add_llvm_example(toyc
  toyc.cpp
  parser/AST.cpp
  mlir/MLIRGen.cpp
  mlir/Dialect.cpp

  DEPENDS
    ToyOpsIncGen
  )

include_directories(include)
include_directories(${CMAKE_CURRENT_BINARY_DIR}/include)
target_link_libraries(toyc
  PRIVATE
    MLIRAnalysis
    MLIRFunctionInterfaces
    MLIRIR
    MLIRParser
    MLIRSideEffectInterfaces
    MLIRTransforms
    )
