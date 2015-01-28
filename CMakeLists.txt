cmake_minimum_required(VERSION 2.8)

# common
project(fastboot)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_C_FLAGS "-std=gnu99 -D_FILE_OFFSET_BITS=64")

# main
add_executable(fastboot
	# fastboot
	protocol.c
	engine.c
	bootimg.c
	fastboot.c
	util.c
	fs.c
	usb_linux.c
	util_linux.c

	# libsparse
	libsparse/backed_block.c
	libsparse/output_file.c
	libsparse/sparse.c
	libsparse/sparse_crc32.c
	libsparse/sparse_err.c
	libsparse/sparse_read.c

	# libzipfile
	libzipfile/zipfile.c
	libzipfile/centraldir.c

	# ext4_utils
	ext4_utils/make_ext4fs.c
	ext4_utils/ext4fixup.c
	ext4_utils/ext4_utils.c
	ext4_utils/allocate.c
	ext4_utils/contents.c
	ext4_utils/extent.c
	ext4_utils/indirect.c
	ext4_utils/uuid.c
	ext4_utils/sha1.c
	ext4_utils/wipe.c
	ext4_utils/crc16.c
	ext4_utils/ext4_sb.c
	ext4_utils/canned_fs_config.c
)
set_property(TARGET fastboot PROPERTY INCLUDE_DIRECTORIES
	${CMAKE_SOURCE_DIR}
	${CMAKE_SOURCE_DIR}/include
	${CMAKE_SOURCE_DIR}/libsparse/include
	${CMAKE_SOURCE_DIR}/ext4_utils
	${CMAKE_SOURCE_DIR}/f2fs_utils
)
target_link_libraries(fastboot z selinux)
