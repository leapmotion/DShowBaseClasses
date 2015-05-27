set(
  BaseClasses_SRCS
  amextra.h
  amfilter.h
  cache.h
  checkbmi.h
  combase.h
  cprop.h
  ctlutil.h
  ddmm.h
  dllsetup.h
  dxmperf.h
  fourcc.h
  measure.h
  msgthrd.h
  mtype.h
  outputq.h
  perflog.h
  perfstruct.h
  pstream.h
  pullpin.h
  refclock.h
  reftime.h
  renbase.h
  schedule.h
  seekpt.h
  source.h
  streams.h
  strmctl.h
  sysclock.h
  transfrm.h
  transip.h
  videoctl.h
  vtrans.h
  winctrl.h
  winutil.h
  wxdebug.h
  wxlist.h
  wxutil.h
  amextra.cpp
  amfilter.cpp
  amvideo.cpp
  arithutil.cpp
  combase.cpp
  cprop.cpp
  ctlutil.cpp
  ddmm.cpp
  dllentry.cpp
  dllsetup.cpp
  mtype.cpp
  outputq.cpp
  perflog.cpp
  pstream.cpp
  pullpin.cpp
  refclock.cpp
  renbase.cpp
  schedule.cpp
  seekpt.cpp
  source.cpp
  strmctl.cpp
  sysclock.cpp
  transfrm.cpp
  transip.cpp
  videoctl.cpp
  vtrans.cpp
  winctrl.cpp
  winutil.cpp
  wxdebug.cpp
  wxlist.cpp
  wxutil.cpp
)

add_pch(BaseClasses_SRCS "stdafx.h" "stdafx.cpp")
add_library(BaseClasses ${BaseClasses_SRCS})
target_include_directories(
  BaseClasses
  INTERFACE
  "$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>"
  "$<INSTALL_INTERFACE:include>"
)
target_link_libraries(BaseClasses Winmm)
set_property(TARGET BaseClasses PROPERTY FOLDER "Pipeline")
set_property(TARGET BaseClasses PROPERTY ARCHIVE_OUTPUT_NAME_DEBUG "BaseClassesd")
install(TARGETS BaseClasses EXPORT BaseClassesTargets
  DESTINATION lib
  COMPONENT baseclasses
  CONFIGURATIONS ${CMAKE_CONFIGURATION_TYPES}
)
