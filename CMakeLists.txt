cmake_minimum_required(VERSION 3.23)

set(PROJECT_NAME faker-cxx)
project(${PROJECT_NAME} CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED YES)

option(BUILD_FAKER_TESTS DEFAULT ON)

if (MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++20 /permissive-")
else ()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -Wconversion -Wformat -Werror")
endif ()

set(LIBRARY_NAME faker-cxx)

set(FAKER_SOURCES
        src/Book.cpp
        src/Color.cpp
        src/Commerce.cpp
        src/Company.cpp
        src/Datatype.cpp
        src/Date.cpp
        src/Finance.cpp
        src/Helper.cpp
        src/Internet.cpp
        src/Location.cpp
        src/Lorem.cpp
        src/Number.cpp
        src/Person.cpp
        src/String.cpp
        src/StringHelper.cpp
        src/Word.cpp
        )

set(FAKER_UT_SOURCES
        src/BookTest.cpp
        src/ColorTest.cpp
        src/CommerceTest.cpp
        src/CompanyTest.cpp
        src/DatatypeTest.cpp
        src/DateTest.cpp
        src/FinanceTest.cpp
        src/InternetTest.cpp
        src/LocationTest.cpp
        src/LoremTest.cpp
        src/NumberTest.cpp
        src/PersonTest.cpp
        src/StringTest.cpp
        src/StringHelperTest.cpp
        src/WordTest.cpp
        )

add_library(${LIBRARY_NAME} ${FAKER_SOURCES})

target_include_directories(${LIBRARY_NAME}
        INTERFACE
        "${CMAKE_CURRENT_LIST_DIR}/include"
        PRIVATE
        "${CMAKE_CURRENT_LIST_DIR}/include"
        )

if (BUILD_FAKER_TESTS)
    add_subdirectory(externals/googletest)

    set(GTEST_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/externals/googletest/googletest/include")

    enable_testing()

    set(target_code_coverage_ALL 1)

    include("cmake/cmake-coverage.cmake")

    add_code_coverage_all_targets()

    add_executable(${LIBRARY_NAME}-UT ${FAKER_UT_SOURCES})

    target_link_libraries(${LIBRARY_NAME}-UT PRIVATE gtest_main faker-cxx)

    target_include_directories(${LIBRARY_NAME}-UT PRIVATE ${GTEST_INCLUDE_DIR} ${CMAKE_CURRENT_LIST_DIR})

    add_test(NAME ${LIBRARY_NAME}-UT COMMAND ${LIBRARY_NAME}-UT WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR})

    target_code_coverage(${LIBRARY_NAME}-UT ALL)
endif ()
