cmake_minimum_required (VERSION 3.16)

project(Application-Example)

file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS 
	"Source/*.h" 
	"Source/*.cpp" 
)

add_executable(Application-Example WIN32 ${SRC_FILES})

source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${SRC_FILES} )

EnableMultiProcessorCompilation(Application-Example)
set_property(TARGET Application-Example PROPERTY CXX_STANDARD 20)
set_property(TARGET Application-Example PROPERTY DEBUG_POSTFIX "")

# Build folder
set_target_properties(Application-Example
	PROPERTIES
	ARCHIVE_OUTPUT_DIRECTORY "${BUILD_FOLDER}/Application-Example"
	LIBRARY_OUTPUT_DIRECTORY "${BUILD_FOLDER}/Application-Example"
	RUNTIME_OUTPUT_DIRECTORY "${BUILD_FOLDER}/Application-Example"
)

target_include_directories(Application-Example PRIVATE 
	"${CMAKE_SOURCE_DIR}/Core" 
	"Source/"
	${THIRD_PARTY_DIR}
	${IMGUI_INCLUDE_DIR}
)

target_link_libraries(Application-Example PRIVATE Core)
