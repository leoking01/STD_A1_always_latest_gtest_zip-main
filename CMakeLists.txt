cmake_minimum_required(VERSION 3.17)
project(gtest_cmake_auto_dwld)





#set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
endif()
#link_directories(${CMAKE_BINARY_DIR} )

message( "CMAKE_C_COMPILER = ${CMAKE_C_COMPILER}"  )
message( "CMAKE_C_COMPILER_VERSION = ${CMAKE_C_COMPILER_VERSION}"  )
message( "CMAKE_CXX_PLATFORM_ID = ${CMAKE_CXX_PLATFORM_ID}"  )
message( "CMAKE_CXX_COMPILER_TARGET = ${CMAKE_CXX_COMPILER_TARGET}"  )
message( "CMAKE_CXX_COMPILER_AR = ${CMAKE_CXX_COMPILER_AR}"  )
message( "CMAKE_C_COMPILER_ABI = ${CMAKE_C_COMPILER_ABI}"  )
message( "CMAKE_C_COMPILER_TARGET = ${CMAKE_C_COMPILER_TARGET}"  )
message( "CMAKE_HOST_SYSTEM = ${CMAKE_HOST_SYSTEM}"  )
message( "CMAKE_HOST_SYSTEM_NAME = ${CMAKE_HOST_SYSTEM_NAME}"  )
message( "CMAKE_VS_PLATFORM_NAME = ${CMAKE_VS_PLATFORM_NAME}"  )
message( "CMAKE_VS_PLATFORM_TOOLSET = ${CMAKE_VS_PLATFORM_TOOLSET}"  )
message( "CMAKE_CXX_COMPILER_VERSION = ${CMAKE_CXX_COMPILER_VERSION}"  )
#message(  "CMAKE_CXX_COMPILER_TARGET= ${CMAKE_CXX_COMPILER_TARGET}"   )
message(  "CMAKE_CXX_COMPILER_ABI= ${CMAKE_CXX_COMPILER_ABI}"   )
message(  "CMAKE_CXX_COMPILER_EXTERNAL_TOOLCHAIN= ${CMAKE_CXX_COMPILER_EXTERNAL_TOOLCHAIN}"   )
message(  "CMAKE_CXX_COMPILER_ID= ${CMAKE_CXX_COMPILER_ID}"   )
message(  "CMAKE_CXX_COMPILER_ARCHITECTURE_ID= ${CMAKE_CXX_COMPILER_ARCHITECTURE_ID}"   )
#message(  "CMAKE_HOST_SYSTEM_NAME= ${CMAKE_HOST_SYSTEM_NAME}"   )
message(  "CMAKE_Fortran_FORMAT= ${CMAKE_Fortran_FORMAT}"   )
message(  "CMAKE_Fortran_COMPILER= ${CMAKE_Fortran_COMPILER}"   )
message(  "CMAKE_Fortran_COMPILER_VERSION= ${CMAKE_Fortran_COMPILER_VERSION}"   )
message(  "CMAKE_Fortran_COMPILER_ID= ${CMAKE_Fortran_COMPILER_ID}"   )


# 改变安装路径可以使用下面的语句，Unix: "/usr/local", Windows: "c:/Program Files/${PROJECT_NAME}" 为默认值，所有的DESTINATION均以此目录为根目录
# set(CMAKE_INSTALL_PREFIX ${CMAKE_BINARY_DIR}/mymath)
#set(CMAKE_INSTALL_PREFIX ${CMAKE_BINARY_DIR}/../${PROJECT_NAME}_${PROJECT_VERSION}_${CMAKE_HOST_SYSTEM}_${CMAKE_CXX_COMPILER_ID}_${CMAKE_CXX_COMPILER_VERSION}_install)
set(CMAKE_INSTALL_PREFIX ${CMAKE_BINARY_DIR}/../${PROJECT_NAME}_${PROJECT_VERSION}_${CMAKE_CXX_COMPILER_ID}_${CMAKE_CXX_COMPILER_VERSION}_${CMAKE_Fortran_COMPILER_ID}_${CMAKE_Fortran_COMPILER_VERSION}_install)








include(FetchContent)
include(CTest)

# （1）  github  master-zip   很容易
#FetchContent_Declare(
#  googletest
#  URL https://github.com/google/googletest/archive/master.zip
##  URL_HASH MD5=5588a7b18261c20068beabfb4f530b87
# SOURCE_DIR  ../googletestLK
#)


# （2） github  tag-zip   很容易
#https://github.com/google/googletest/archive/refs/tags/v1.12.0.zip
#https://codeload.github.com/google/googletest/zip/refs/tags/v1.12.0
#message( "start to download from : https://codeload.github.com/google/googletest/zip/refs/tags/v1.12.0 ")
#FetchContent_Declare(
#  googletest
#  URL https://codeload.github.com/google/googletest/zip/refs/tags/v1.12.0
##  URL_HASH MD5=5588a7b18261c20068beabfb4f530b87
# SOURCE_DIR  ../googletestLK
#)

# （3） gitee  zip   很容易
#https://gitee.com/LSLWIND/googletest/repository/archive/master.zip
#https://gitee.com/LSLWIND/googletest/repository/blazearchive/master.zip?Expires=1667013190&Signature=VcaPS18VhEpoXpmubfbDV3QscBd0KCSWDLk85QgIzpU%3D
#message( " gitee  zip , start to download from : https://codeload.github.com/google/googletest/zip/refs/tags/v1.12.0 ")
#FetchContent_Declare(
#  googletest
#  URL https://codeload.github.com/google/googletest/zip/refs/tags/v1.12.0
##  URL_HASH MD5=5588a7b18261c20068beabfb4f530b87
# SOURCE_DIR  ../googletestLKGitee
#)

# （4） github  git   很容易
##https://gitee.com/LSLWIND/googletest.git
message( "start to download from : https://gitee.com/LSLWIND/googletest.git ")
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://gitee.com/LSLWIND/googletest.git
#  URL_HASH MD5=5588a7b18261c20068beabfb4f530b87
 SOURCE_DIR  ../googletestLK_GITEE_git
)

#  （5） github  git   极难下载  完全取决于网速、连接情况
#message( "start to download from : https://github.com/google/googletest.git ")
#FetchContent_Declare(
#  googletest
#  GIT_REPOSITORY https://github.com/google/googletest.git
##  GIT_TAG        703bd9caab50b139428cea1aaff9974ebee5742e # release-1.10.0
#  SOURCE_DIR  ../googletestLK_github_git
#)



FetchContent_MakeAvailable(googletest)

# Now simply link against gtest or gtest_main as needed.
add_executable(example example.cpp)
target_link_libraries(example 
	gtest_main 
	gmock 
)

add_test(NAME example_test COMMAND example)
