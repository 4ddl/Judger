cmake_minimum_required(VERSION 2.5)
project(measure C)

#set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/output)

set(CMAKE_C_FLAGS "-g -Wall -Werror -O3 -std=c99 -pie -fPIC")

# make measure lib
file(GLOB SOURCE "src/*.c" "src/rules/*.c")
add_executable(measure ${SOURCE})
target_link_libraries(measure pthread seccomp)


install(TARGETS measure
	PERMISSIONS OWNER_EXECUTE OWNER_READ GROUP_EXECUTE GROUP_READ WORLD_EXECUTE WORLD_READ
	RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
install(FILES policy/java_policy
	PERMISSIONS OWNER_WRITE OWNER_READ GROUP_READ WORLD_READ
	DESTINATION /etc)
