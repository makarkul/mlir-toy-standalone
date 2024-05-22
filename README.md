# mlir-toy-standalone
This repository replicates the [Toy tutorial](https://mlir.llvm.org/docs/Tutorials/Toy) which is provided with MLIR, in stand-alone more. The motivation was to provide user steps to replicate each chapter of the tutorial and at points substeps as you add the required details to the Toy language.

## Build
It is expected that the user has successfully cloned and built LLVM project as given in the [Getting Started with MLIR](https://mlir.llvm.org/getting_started) page. Once build is successful, we export the build locations to be used further in this tutorial build.
```
export LLVM_BUILD_DIR=$HOME/llvm-project-main/build
```
Build the Toy example in the top folder of this repository as follows:
```
mkdir -p build && cd build
cmake -G Ninja .. \
    -DLLVM_DIR=$LLVM_BUILD_DIR/lib/cmake/llvm \
    -DMLIR_DIR=$LLVM_BUILD_DIR/lib/cmake/mlir

cmake --build . --target toyc
```
For `tablegen` use target `ToyOpsIncGen`. Rest of the instructions follow the ones given in the original tutorial

