cmake_minimum_required(VERSION 3.9)

project(Daytime1-Source_Listing)

if(MSVC)
  set(DLLIMPORT "__declspec(dllimport)")
  set(DLLEXPORT "__declspec(dllexport)")
  set(DISABLE "__pragma(warning(push,0))")
  set(ENABLE "__pragma(warning(pop))")
endif()

set(PROJECT_SRCS
${PROJECT_SOURCE_DIR}/src/Daytime1-Source_Listing.cpp
)



source_group("src" FILES ${PROJECT_SRCS})
find_package( Boost COMPONENTS filesystem system asio REQUIRED )


add_executable(${PROJECT_NAME} ${PROJECT_SRCS})

target_link_libraries(${PROJECT_NAME} hvr_sample
                                      Boost::filesystem
                                      Boost::system
                                      Boost::asio)

set_property(TARGET ${PROJECT_NAME} PROPERTY FOLDER ${CMAKE_PROJECT_NAME}/apps)

install(TARGETS ${PROJECT_NAME}
        EXPORT ${CMAKE_PROJECT_NAME}Targets
        DESTINATION bin COMPONENT install-app)
