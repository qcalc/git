cmake_minimum_required(VERSION 3.5)
PROJECT(git)

SET(CMAKE_BUILD_TYPE Debug)

find_package(OpenSSL REQUIRED)
find_package(ZLIB REQUIRED)

INCLUDE_DIRECTORIES(.
        ${OPENSSL_INCLUDE_DIR}
        ${ZLIB_INCLUDE_DIR})

# read-cache
add_library(read-cache read-cache.c cache.h)
target_link_libraries(read-cache
        ${OPENSSL_LIBRARIES}
        ${ZLIB_LIBRARIES})

# init-db
add_executable(init-db init-db.c)
target_link_libraries(init-db read-cache)

# update-cache
add_executable(update-cache update-cache.c)
target_link_libraries(update-cache read-cache)

# show-diff
add_executable(show-diff show-diff.c)
target_link_libraries(show-diff read-cache)

# write-tree
add_executable(write-tree write-tree.c)
target_link_libraries(write-tree read-cache)

# read-tree
add_executable(read-tree read-tree.c)
target_link_libraries(read-tree read-cache)

# commit-tree
add_executable(commit-tree commit-tree.c)
target_link_libraries(commit-tree read-cache)

# cat-file
add_executable(cat-file cat-file.c)
target_link_libraries(cat-file read-cache)