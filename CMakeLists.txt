cmake_minimum_required(VERSION 3.20)

project(carticulate LANGUAGES CXX)

find_package(Python REQUIRED COMPONENTS Interpreter Development.Module)
find_package(pybind11 REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(fmt REQUIRED)
find_package(g2o REQUIRED)

pybind11_add_module(carticulate

    pybind/pybind.cpp
    pybind/utils.cpp

    dynamics/dynamic_armature.cpp
    dynamics/dynamic_model.cpp

    kinematics/kinematic_armature.cpp
    kinematics/kinematic_model.cpp
    kinematics/kinematic_optimizer.cpp

    imu/detector.cpp
    imu/eskf_imu.cpp
)

target_link_libraries(carticulate PRIVATE
    Eigen3::Eigen
    fmt::fmt
    g2o::core
    g2o::stuff
)

target_compile_features(carticulate PRIVATE cxx_std_17)