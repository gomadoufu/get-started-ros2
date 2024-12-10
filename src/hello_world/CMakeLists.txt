cmake_minimum_required(VERSION 3.8)
project(hello_world)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# C++17の設定
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif()

# 依存パッケージ
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(hello_world_msgs REQUIRED)

# ビルド設定の便利関数
function(custom_executable target)
  add_executable(${target} src/${target}.cpp)
  ament_target_dependencies(${target} "hello_world_msgs")
  install(TARGETS ${target} DESTINATION lib/${PROJECT_NAME})
endfunction()

# talkerノードのビルド設定
custon_executable(talker)
# listenerノードのビルド設定
custom_executable(listener)

ament_package()
