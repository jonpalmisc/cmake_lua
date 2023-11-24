cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(lua VERSION 5.4.6 LANGUAGES C)

option(LUA_BUILD_COMPILER "Build the Lua compiler" ON)
option(LUA_BUILD_INTERPRETER "Build the Lua interpreter" ON)

add_library(lua
  lapi.c
  lcode.c
  lctype.c
  ldebug.c
  ldo.c
  ldump.c
  lfunc.c
  lgc.c
  llex.c
  lmem.c
  lobject.c
  lopcodes.c
  lparser.c
  lstate.c
  lstring.c
  ltable.c
  ltm.c
  lundump.c
  lvm.c
  lzio.c
  lauxlib.c
  lbaselib.c
  lcorolib.c
  ldblib.c
  liolib.c
  lmathlib.c
  loadlib.c
  loslib.c
  lstrlib.c
  ltablib.c
  lutf8lib.c
  linit.c)

target_include_directories(lua PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_features(lua PRIVATE c_std_99)

add_library(lua::lang ALIAS lua)

if(LUA_BUILD_COMPILER)
  add_executable(luac luac.c)
  target_link_libraries(luac PRIVATE lua)

  add_executable(lua::compiler ALIAS luac)
endif()

if(LUA_BUILD_INTERPRETER)
  add_executable(luai lua.c)
  target_link_libraries(luai PRIVATE lua)

  add_executable(lua::interpreter ALIAS luai)
endif()
