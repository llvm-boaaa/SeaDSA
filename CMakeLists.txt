file(GLOB SEA_DSA_HEADERS
	"${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/sea_dsa/*.h"
	"${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/sea_dsa/*.hh"
	"${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/sea_dsa/support/*.h"
	"${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/sea_dsa/support/*.hh"
)

file(GLOB SEA_DSA_SOURCES
	"${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/src/*.cc"
)

add_library(SEA_DSA ${SEA_DSA_HEADERS} ${SEA_DSA_SOURCES})

if (CUSTOM_BOOST_1_55_ROOT)
    set (BOOST_ROOT ${CUSTOM_BOOST_1_55_ROOT})
    set (Boost_NO_SYSTEM_PATHS "ON")
endif()

find_package (Boost 1.55)
if (Boost_FOUND)
    
else()
	message(FATAL_ERROR "BOOST 1.55 not found, needed for Sea-Dsa")
endif ()

target_include_directories(SEA_DSA PUBLIC "${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/" ${Boost_INCLUDE_DIRS})

#add LLVM_50 wrapper and mark SEA_DSA lib as dependencie of lv.50
boaaa_add_analysis(NAME SEA_DSA VERSION "50" MAKRO "SEA_DSA" INCLUDE_DIRS "${Boost_INCLUDE_DIRS};${BOAAA_SOURCE_DIR}/analysis/Sea-Dsa/include/")