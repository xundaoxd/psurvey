get_property(dialect_libs GLOBAL PROPERTY MLIR_DIALECT_LIBS)
get_property(conversion_libs GLOBAL PROPERTY MLIR_CONVERSION_LIBS)
get_property(extension_libs GLOBAL PROPERTY MLIR_EXTENSION_LIBS)

file(GLOB SRCS *.cpp)
add_llvm_executable(demo-opt ${SRCS})
target_link_libraries(demo-opt
    PRIVATE
        ${dialect_libs}
        ${conversion_libs}
        ${extension_libs}
        MLIROptLib)
