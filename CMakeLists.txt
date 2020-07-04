cmake_minimum_required(VERSION 3.17)
project(notifyme)

# Configuring python/venv/pip
find_package(Python3 REQUIRED COMPONENTS Interpreter)
set (VENV ${CMAKE_BINARY_DIR}/venv)
set (REQUIREMENTS ${CMAKE_SOURCE_DIR}/python/requirements.txt)

set (BIN_DIR ${VENV}/bin)
set (PYTHON ${BIN_DIR}/python)

add_custom_command(
	OUTPUT ${PYTHON}
	COMMAND ${Python3_EXECUTABLE} -m venv ${VENV}
	COMMAND ${BIN_DIR}/pip install -r ${REQUIREMENTS} --upgrade)

add_custom_target(venv DEPENDS ${PYTHON} ${REQUIREMENTS})

add_executable(main main.cpp)
add_dependencies(main venv)
