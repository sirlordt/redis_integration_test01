# redis_integration_test01

# Fixed

Demo to get *"Segmentation fault (core dumped)"* when the binary is full static option *-static* is used by the linker

# You must has installed conan/python wide system:

## To check conan is installed and working

```
  $ conan --version
```

## To install conan using pip (Package manager from phyton):

```
  $ pip conan
```

## Clone the repo and run in the root folder of project

```
  redis_integration_tes01$ ./run_build_debug.sh make
```

# 2022-05-07 - Fixed

Read the next:

[https://github.com/sewenew/redis-plus-plus/issues/356](https://github.com/sewenew/redis-plus-plus/issues/356)
[https://stackoverflow.com/questions/9002264/starting-a-stdthread-with-static-linking-causes-segmentation-fault](https://stackoverflow.com/questions/9002264/starting-a-stdthread-with-static-linking-causes-segmentation-fault)

pthread cause segmenetation fault you mus add -Wl,--whole-archive pthread -Wl,--no-whole-archive

to the linker options

```cmake
target_link_libraries( ${PROJECT_NAME} PRIVATE -Wl,--whole-archive pthread -Wl,--no-whole-archive PACKAGE_MANAGER_CONAN_LIBS )
```
