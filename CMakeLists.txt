# ================              pro_sqllite  ( example how include and use sqllite)    =========================
cmake_minimum_required(VERSION 3.13 FATAL_ERROR)



set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# default to Release build (it's what most people will use, except cegui devs)
#=====================set kind of build: Debug  +++++++====================== 
if (NOT CMAKE_BUILD_TYPE)
    set( CMAKE_BUILD_TYPE Debug CACHE STRING "Sets the configuration to build (Release, Debug, etc...)")
endif()
#============================================================================




# set parth to the modules which find Postgresql
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")

# made some flag to add for lib pqxx for compiler
# set(SOME_COMPILER_CFLAGS "-lpqxx -lpq")
# set(PQXX /usr/include/pqxx)


#sets names for project
set (PROJECT_NAME  pro_sandbox)
#sets names for aplication
#set (PROJECT_NAME  pro_sandbox3types)




# var for application for create and write
set(APP_CREATE    Timber_Game)


#set name for project
project(${PROJECT_NAME} )



# add some flags for build
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lrt")
# add_subdirectory(3rdparty/SFML)

set( SOURCE_CREATE
     src/source/Ball.cpp 
     src/source/Bat.cpp 
     src/source/main.cpp
   )



set( HEADERS
     #src/include/sample_draw_text.hpp
     #src/include/myTypes.h
     #src/include/Data.h
     
     src/include/Ball.h 
     src/include/Bat.h
    )

# make application  for create
add_executable(
                 ${APP_CREATE}

                 ${HEADERS}
                 ${SOURCE_CREATE}
              )






target_compile_features(${APP_CREATE}      PRIVATE cxx_std_20)





#make include for include directories
target_include_directories(
                                  ${APP_CREATE}
                                  PRIVATE
                                  "src/include"
                           )

#


set_target_properties( ${APP_CREATE}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
   
)


#-- set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
#-- set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
#-- set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
#-- set(RESOURCE_DIRECTORY ${CMAKE_BINARY_DIR}/fonts)


option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

message("--!!! path to build : ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}" )
message("--!!! path to fonts : ${RESOURCE_DIRECTORY}" )


set(SOURCE_DIRECTORY_FONTS ${CMAKE_CURRENT_SOURCE_DIR}/src/fonts)
set(DESTINATION_DIRECTORY_FONTS ${CMAKE_BINARY_DIR}/bin)

set(SOURCE_DIRECTORY_SOUND ${CMAKE_CURRENT_SOURCE_DIR}/src/sound)
set(DESTINATION_DIRECTORY_SOUND ${CMAKE_BINARY_DIR}/bin)

# -- set(SOURCE_DIRECTORY_GRAPHICS ${CMAKE_CURRENT_SOURCE_DIR}/src/graphics)
# -- set(DESTINATION_DIRECTORY_GRAPHICS ${CMAKE_BINARY_DIR}/bin)
# -- 
# -- set(SOURCE_DIRECTORY_GAMEDATA ${CMAKE_CURRENT_SOURCE_DIR}/src/gamedata)
# -- set(DESTINATION_DIRECTORY_GAMEDATA ${CMAKE_BINARY_DIR}/bin)



#file(COPY ${SOURCE_DIRECTORY_FONTS}/Arial.TTF   DESTINATION ${DESTINATION_DIRECTORY_FONTS} )
file(COPY ${SOURCE_DIRECTORY_FONTS}    DESTINATION ${DESTINATION_DIRECTORY_FONTS}    )
#-- file(COPY ${SOURCE_DIRECTORY_GRAPHICS} DESTINATION ${DESTINATION_DIRECTORY_GRAPHICS} )
file(COPY ${SOURCE_DIRECTORY_SOUND}    DESTINATION ${DESTINATION_DIRECTORY_SOUND}    )
# -- file(COPY ${SOURCE_DIRECTORY_GAMEDATA} DESTINATION ${DESTINATION_DIRECTORY_GAMEDATA} )

#============  SFML [1]===============================
add_subdirectory(3rdparty/SFML)
find_package(fmt REQUIRED)

# Поиск пакета SFML
# Укажите SFML_DIR, если SFML установлена в нестандартном месте
#find_package(SFML 2.6 COMPONENTS graphics REQUIRED) # дополните нужными вам модулями


# Связывание с библиотеками SFML
target_link_libraries(${APP_CREATE} sfml-system sfml-graphics sfml-window  sfml-audio sfml-network  fmt::fmt)  



#============  SFML [2]===============================
