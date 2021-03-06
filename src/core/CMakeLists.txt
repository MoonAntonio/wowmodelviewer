cmake_minimum_required(VERSION 2.6)
include(${CMAKE_CURRENT_LIST_DIR}/../cmake/common.cmake)

project(core)

message(STATUS "Building nextgen Core")

include_directories(.)

# Qt5 stuff
find_package(Qt5Core) 
find_package(Qt5Gui) # Qt5Gui is needed for QImage
find_package(Qt5Network)
find_package(Qt5Xml)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)

set(src CharInfos.cpp
		CSVFile.cpp
		dbfile.cpp
        ExporterPlugin.cpp
        FileDownloader.cpp
		Game.cpp
		GameDatabase.cpp
		GameFile.cpp
		GameFolder.cpp
        GlobalSettings.cpp
        ImporterPlugin.cpp
		MemoryUtils.cpp
        Model.cpp
        NPCInfos.cpp
        Plugin.cpp
        PluginManager.cpp
        VersionManager.cpp
        metaclasses/Component.cpp
        metaclasses/Event.cpp
        metaclasses/Observable.cpp
        metaclasses/Observer.cpp
        logger/Logger.cpp
        logger/LogOutputConsole.cpp
        logger/LogOutputFile.cpp)

set(headers CharInfos.h
			CSVFile.h
			dbfile.h
			ExporterPlugin.h
			FileDownloader.h
			Game.h
			GameDatabase.h
			GameFile.h
			GameFolder.h
			GlobalSettings.h
			ImporterPlugin.h
			MemoryUtils.h
			Model.h
			NPCInfos.h
			Plugin.h
			PluginManager.h
			VersionManager.h
			metaclasses/BaseIterator.h
			metaclasses/Component.h
			metaclasses/Container.h
			metaclasses/Event.h
			metaclasses/Observable.h
			metaclasses/Observer.h
			logger/Logger.h
			logger/LogOutput.h
			logger/LogOutputConsole.h
			logger/LogOutputFile.h)

source_group("Header Files" FILES ${headers})
			
use_glew()
use_cximage()
use_sqlite()

add_definitions(-DBUILDING_CORE_DLL)

add_library(core SHARED ${src} ${headers})
set_property(TARGET core PROPERTY FOLDER "libraries")

target_link_libraries(core Qt5::Core Qt5::Network Qt5::Xml Qt5::Gui ${extralibs})

if(WIN32)
  install(TARGETS core RUNTIME DESTINATION "${WMV_BASE_PATH}/bin/")
endif(WIN32)
