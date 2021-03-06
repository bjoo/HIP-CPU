set(name bit_extract)

add_executable(${name} bit_extract.cpp)

if (${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
    target_compile_options(
        ${name} PRIVATE
            /arch:AVX2
            /openmp:experimental
            /permissive-
            /Qvec-report:2
            /Zc:preprocessor)
    target_compile_definitions(${name} PRIVATE WIN32_LEAN_AND_MEAN NOMINMAX)
else ()
    target_compile_options(${name} PRIVATE -Wall -fopenmp-simd)
    target_link_libraries(${name} PRIVATE dl tbb)
endif ()
target_include_directories(
    ${name} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../../include)
target_link_libraries(${name} PRIVATE Threads::Threads)