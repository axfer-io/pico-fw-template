add_library(app_src OBJECT
    main.c
)

target_include_directories(app_src PUBLIC ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(app_src PRIVATE
    pico_stdlib
    drivers
    utils
)
