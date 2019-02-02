cmake_minimum_required(VERSION 2.8)

SET(COMPILE_DEFINITIONS -Werror)
SET(CMAKE_EXE_LINKER_FLAGS "-Wl,--copy-dt-needed-entries")

include_directories(/sdc/raspberrypi/firmware-master/opt/vc/include)
include_directories(/sdc/raspberrypi/firmware-master/opt/vc/include/interface/vcos/pthreads)
include_directories(/sdc/raspberrypi/firmware-master/opt/vc/include/interface/vmcs_host)
include_directories(/sdc/raspberrypi/firmware-master/opt/vc/include/interface/vmcs_host/linux)

include_directories(/home/pi/src/raspberrypi/userland)
include_directories(/sdc/raspberrypi/firmware-master/opt/vc/src/hello_pi/libs/vgfont)

link_directories(/sdc/raspberrypi/firmware-master/opt/vc/lib)
link_directories(/sdc/raspberrypi/firmware-master/opt/vc/src/hello_pi/libs/vgfont)

add_executable(mmaldemo main.cpp)
add_executable(mmal_buffer_demo buffer_demo.cpp)
add_executable(mmal_opencv_demo opencv_demo.cpp)
add_executable(mmal_video_record video_record.cpp)

find_package( OpenCV REQUIRED )


target_link_libraries(mmaldemo mmal_core mmal_util mmal_vc_client vcos bcm_host)
target_link_libraries(mmal_buffer_demo mmal_core mmal_util mmal_vc_client vcos bcm_host rt)
target_link_libraries(mmal_opencv_demo mmal_core mmal_util mmal_vc_client vcos bcm_host ${OpenCV_LIBS} vgfont openmaxil brcmGLESv2 EGL brcmEGL pthread rt m freetype)
target_link_libraries(mmal_video_record mmal_core mmal_util mmal_vc_client vcos bcm_host cairo rt)
