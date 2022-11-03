cmake_minimum_required(VERSION 3.21)
project(CppGame LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(SFML
        GIT_REPOSITORY https://github.com/SFML/SFML.git
        GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

add_executable(
        CppGame
        src/main.cpp
        src/SceneManager/scene.hpp src/SceneManager/scene.cpp
        src/SceneManager/spriteObject.hpp src/SceneManager/spriteObject.cpp
        src/SceneManager/sceneHandler.hpp src/SceneManager/sceneHandler.cpp
        src/SceneManager/gameObject.hpp src/SceneManager/gameObject.cpp
        src/SceneManager/button.hpp src/SceneManager/button.cpp
        src/SceneManager/character.hpp src/SceneManager/character.cpp
        src/SceneManager/quitButton.hpp src/SceneManager/quitButton.cpp
        src/SceneManager/textObject.hpp src/SceneManager/textObject.cpp
)

target_link_libraries(CppGame PRIVATE sfml-graphics)
target_compile_features(CppGame PRIVATE cxx_std_17)
if (WIN32 AND BUILD_SHARED_LIBS)
    add_custom_command(TARGET CppGame POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:CppGame> $<TARGET_FILE_DIR:CppGame> COMMAND_EXPAND_LISTS)
endif()

install(TARGETS CppGame)