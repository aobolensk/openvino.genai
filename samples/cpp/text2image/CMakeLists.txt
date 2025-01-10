find_package(OpenVINOGenAI REQUIRED
    PATHS
        "${CMAKE_BINARY_DIR}"  # Reuse the package from the build.
        ${OpenVINO_DIR}  # GenAI may be installed alogside OpenVINO.
    NO_CMAKE_FIND_ROOT_PATH
)

add_executable(txt2image_from_subcomponent
${CMAKE_CURRENT_SOURCE_DIR}/txt2image_from_subcomponent.cpp
${CMAKE_CURRENT_SOURCE_DIR}/imwrite.cpp)

target_include_directories(txt2image_from_subcomponent PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(txt2image_from_subcomponent PRIVATE openvino::genai)

set_target_properties(txt2image_from_subcomponent PROPERTIES
COMPILE_PDB_NAME txt2image_from_subcomponent
# Ensure out of box LC_RPATH on macOS with SIP
INSTALL_RPATH_USE_LINK_PATH ON)

install(TARGETS txt2image_from_subcomponent
    RUNTIME DESTINATION samples_bin/
    COMPONENT samples_bin
    EXCLUDE_FROM_ALL)