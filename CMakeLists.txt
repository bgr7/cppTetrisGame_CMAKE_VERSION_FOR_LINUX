cmake_minimum_required(VERSION 3.16)
project(bugraBaygul20190705005-072 LANGUAGES CXX)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

add_executable(bugraBaygul20190705005-072 main.cpp Game.cpp Color.cpp Position.cpp Pieces.cpp Piece.cpp Board.cpp)

target_link_libraries(bugraBaygul20190705005-072 PRIVATE sfml-graphics sfml-audio)
target_compile_features(bugraBaygul20190705005-072 PRIVATE cxx_std_17)

if(WIN32)
    add_custom_command(
        TARGET bugraBaygul20190705005-072
        COMMENT "Copy OpenAL DLL"
        PRE_BUILD COMMAND ${CMAKE_COMMAND} -E copy ${SFML_SOURCE_DIR}/extlibs/bin/$<IF:$<EQUAL:${CMAKE_SIZEOF_VOID_P},8>,x64,x86>/openal32.dll $<TARGET_FILE_DIR:bugraBaygul20190705005-072>
        VERBATIM)
endif()


# Copy the font file to the output directory
configure_file(Font/roboto.ttf ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Font/roboto.ttf COPYONLY)

# Copy the score file to the output directory
configure_file(Score/sb.txt ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Score/sb.txt COPYONLY)

# Copy the sound files to the output directory
configure_file(Sounds/clear.mp3 ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Sounds/clear.mp3 COPYONLY)
configure_file(Sounds/gameover.mp3 ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Sounds/gameover.mp3 COPYONLY)
configure_file(Sounds/hard.mp3 ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Sounds/hard.mp3 COPYONLY)
configure_file(Sounds/music.mp3 ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Sounds/music.mp3 COPYONLY)
configure_file(Sounds/rotate.mp3 ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Sounds/rotate.mp3 COPYONLY)

install(TARGETS bugraBaygul20190705005-072)
