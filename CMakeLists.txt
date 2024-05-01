cmake_minimum_required(VERSION 3.29.0) 
project(NETNEST VERSION 0.0.1 DESCRIPTION "Simple embedded HTTP server" LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)

set(BINARY_NAME ${PROJECT_NAME})   

set(ESP_HTTP_LIB "esphttp")
set(ESP_HTTP_PATH "D:/esp-idf/components/esp_http_server")
include_directories(${ESP_HTTP_PATH}/include)

# Add source files of esp_http_server
file(GLOB_RECURSE ESP_HTTP_SRCS ${ESP_HTTP_PATH}/src/*.c)

# Add esp_http_server as a library
add_library(${ESP_HTTP_LIB} STATIC ${ESP_HTTP_SRCS})


# Add executable
add_executable(${BINARY_NAME} 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/core/nethttp.cpp
)

target_include_directories(${BINARY_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src/core/include)
set_target_properties(${ESP_HTTP_LIB} PROPERTIES LINKER_LANGUAGE C)
# Link libraries
target_link_libraries(${BINARY_NAME} PUBLIC ${ESP_HTTP_LIB})

