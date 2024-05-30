cmake_minimum_required(VERSION 3.22)

project(mlir-toy LANGUAGES CXX C)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
include(MLIRToy)

add_subdirectory(include)

set(LLVM_LINK_COMPONENTS
  Support
  )

set(LLVM_TARGET_DEFINITIONS mlir/ToyCombine.td)
mlir_tablegen(ToyCombine.inc -gen-rewriters)
add_public_tablegen_target(ToyCombineIncGen)

add_llvm_example(toyc
  toyc.cpp
  parser/AST.cpp
  mlir/MLIRGen.cpp
  mlir/Dialect.cpp
  mlir/LowerToAffineLoops.cpp
  mlir/ShapeInferencePass.cpp
  mlir/ToyCombine.cpp

  DEPENDS
  ToyShapeInferenceInterfaceIncGen
  ToyOpsIncGen
  ToyCombineIncGen
  )

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR}/include)
get_property(dialect_libs GLOBAL PROPERTY MLIR_DIALECT_LIBS)
get_property(extension_libs GLOBAL PROPERTY MLIR_EXTENSION_LIBS)
target_link_libraries(toyc
  PRIVATE
    ${dialect_libs}
    ${extension_libs}
    MLIRAnalysis
    MLIRCallInterfaces
    MLIRCastInterfaces
    MLIRFunctionInterfaces
    MLIRIR
    MLIRParser
    MLIRPass
    MLIRSideEffectInterfaces
    MLIRSupport
    MLIRTransforms
    )
