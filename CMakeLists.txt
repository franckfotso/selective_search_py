cmake_minimum_required(VERSION 2.8)

project(selective_search)

execute_process(COMMAND python2.7-config --cflags  OUTPUT_VARIABLE PYTHON2.7_CFLAGS  OUTPUT_STRIP_TRAILING_WHITESPACE)
execute_process(COMMAND python2.7-config --ldflags OUTPUT_VARIABLE PYTHON2.7_LDFLAGS OUTPUT_STRIP_TRAILING_WHITESPACE)

set(BOOST_LIBS "-lboost_system -lboost_python -lboost_numpy")

set(SUPPRESS_WARNING "-Wall -Wno-unused-function -Wno-unused-variable -Wno-unused-local-typedefs")

include_directories("segment" "/root/.virtualenvs/rfm/include/python2.7/" "/opt/Boost.NumPy")
set(CMAKE_CXX_FLAGS "-fPIC -O3 -std=c++11 ${PYTHON2.7_CFLAGS} ${SUPPRESS_WARNING}")
set(CMAKE_SHARED_LINKER_FLAGS "${PYTHON2.7_LDFLAGS} -shared -fPIC")

add_library(segment SHARED segment_py.cpp)
target_link_libraries(segment ${BOOST_LIBS} segment)
set_target_properties(segment PROPERTIES PREFIX "")
