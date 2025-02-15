add_executable(tests
    common/bit_field.cpp
    common/param_package.cpp
    core/arm/arm_test_common.cpp
    core/arm/arm_test_common.h
    core/arm/dyncom/arm_dyncom_vfp_tests.cpp
    core/core_timing.cpp
    core/file_sys/path_parser.cpp
    core/hle/kernel/hle_ipc.cpp
    core/memory/memory.cpp
    core/memory/vm_manager.cpp
    audio_core/audio_fixures.h
    audio_core/decoder_tests.cpp
)

if (ARCHITECTURE_x86_64)
    target_sources(tests
        PRIVATE
            video_core/shader/shader_jit_x64_compiler.cpp
    )
endif()

create_target_directory_groups(tests)

target_link_libraries(tests PRIVATE common core video_core audio_core)
target_link_libraries(tests PRIVATE ${PLATFORM_LIBRARIES} Catch2::Catch2WithMain nihstro-headers Threads::Threads)

add_test(NAME tests COMMAND tests)
