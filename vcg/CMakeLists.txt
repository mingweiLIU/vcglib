#filety 例如：*.h
function(installfilesindir basedir abusolutedir filetype)
    file(GLOB children RELATIVE ${abusolutedir} ${abusolutedir}/*)
    foreach(child ${children})
        if(IS_DIRECTORY ${abusolutedir}/${child} )
            installfilesindir(${basedir} ${abusolutedir}/${child} ${filetype})
        endif()
        #拷贝外面的数据
        file(GLOB relativepath RELATIVE ${basedir} ${abusolutedir})
        file(GLOB dirfiles "${abusolutedir}/${child}/${filetype}")
        install(FILES ${dirfiles} DESTINATION include/${relativepath}/${child} COMPONENT Development)
    endforeach()    
endfunction()

installfilesindir(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR} "*.h")