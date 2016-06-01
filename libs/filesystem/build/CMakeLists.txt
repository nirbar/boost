CMAKE_MINIMUM_REQUIRED (VERSION 3.4)


PROJECT (boost_fs)

INCLUDE_DIRECTORIES ( 
	../../../
	)

ADD_DEFINITIONS(-DBOOST_ALL_NO_LIB)
SET( CMAKE_POSITION_INDEPENDENT_CODE True)

# Platform specific compilation flags
IF (MSVC)
	OPTION( STATIC_CRT		"Link the static CRT libraries"	ON  )
	IF(STATIC_CRT)
		FOREACH(flag_var
				CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE
				CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
			IF(${flag_var} MATCHES "/MD")
				STRING(REGEX REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
			ENDIF(${flag_var} MATCHES "/MD")
		ENDFOREACH(flag_var)
	ENDIF()
ENDIF()

SET( BOOST_FS_SOURCES
	../src/codecvt_error_category.cpp
	../src/operations.cpp
	../src/path.cpp
	../src/path_traits.cpp
	../src/portability.cpp
	../src/unique_path.cpp
	../src/utf8_codecvt_facet.cpp
	../src/windows_file_codecvt.cpp
	../../system/src/error_code.cpp
	)

ADD_LIBRARY(boost_fs STATIC ${BOOST_FS_SOURCES})
