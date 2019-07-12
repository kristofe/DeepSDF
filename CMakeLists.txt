project("DeepSDF")
cmake_minimum_required(VERSION 3.0)

#find_package(CLI11 CONFIG REQUIRED)

LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/third-party/eigen/cmake/")
#message(${CMAKE_MODULE_PATH})

include_directories("third-party/nanoflann/include")
include_directories("third-party/CLI11/include")
#add_subdirectory(third-party/CLI11/build)
#find_package(CLI11 CONFIG)
find_package(Eigen3 REQUIRED)
#find_package(nanoflann REQUIRED)
find_package(Pangolin REQUIRED)

add_subdirectory(third-party/cnpy)



set(SOURCES
    src/ShaderProgram.cpp
    src/Utils.cpp)

add_executable(PreprocessMesh src/PreprocessMesh.cpp ${SOURCES})
target_include_directories(PreprocessMesh PRIVATE third-party/cnpy)
#target_link_libraries(PreprocessMesh PRIVATE CLI11::CLI11 pangolin cnpy Eigen3::Eigen nanoflann::nanoflann)
target_link_libraries(PreprocessMesh PRIVATE pangolin cnpy)
target_compile_features(PreprocessMesh PRIVATE cxx_std_14)
set_target_properties(PreprocessMesh PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")

add_executable(SampleVisibleMeshSurface src/SampleVisibleMeshSurface.cpp ${SOURCES})
target_include_directories(SampleVisibleMeshSurface PRIVATE third-party/cnpy)
#target_link_libraries(SampleVisibleMeshSurface PRIVATE CLI11::CLI11 pangolin cnpy Eigen3::Eigen nanoflann::nanoflann)
target_link_libraries(SampleVisibleMeshSurface PRIVATE pangolin cnpy)
target_compile_features(SampleVisibleMeshSurface PRIVATE cxx_std_14)
set_target_properties(SampleVisibleMeshSurface PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")
