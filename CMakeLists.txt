PROJECT( IntroToD3D9 )
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

FILE(GLOB_RECURSE srcList "*.cpp")

# fliter duplicates projects
FOREACH(src ${srcList})
        MESSAGE("finded: " ${src})
        STRING( REGEX REPLACE "(.*/.*)/.*\\.cpp$" "\\1" dirName ${src} )
        LIST(APPEND dirNameList ${dirName})
        MESSAGE("directory Finded: " ${dirName} )
ENDFOREACH(src ${srcList})

MESSAGE("..................................................................")

LIST(REMOVE_DUPLICATES dirNameList)

FOREACH(dir ${dirNameList})
        MESSAGE( ${dir} " Process begin.....")
        STRING( REGEX REPLACE ".*/(.*)" "\\1" prjName ${dir} )
        FILE(GLOB prjSrcList "${dir}/*.cpp" "${dir}/*.h")

        FOREACH(prjSrc ${prjSrcList})
                MESSAGE("src glob: " ${prjSrc})
        ENDFOREACH(prjSrc)

        MESSAGE("before replace Project: " ${prjName} )
        STRING( REPLACE " " "" prj ${prjName})
        ADD_EXECUTABLE( ${prj} ${prjSrcList} )

        MESSAGE("Added Project: " ${prj} )
        SET_TARGET_PROPERTIES(${prj} PROPERTIES WIN32_EXECUTABLE "true")
        TARGET_LINK_LIBRARIES(${prj} d3d9 d3dx9 winmm)

ENDFOREACH(dir ${dirName})
