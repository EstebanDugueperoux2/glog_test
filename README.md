# glog_test

## Test with conan 1.59.0

```
conan new boost_test/0.0.1 --template=cmake_lib
#Add glog to requirement
#Add "#include <glog/logging.h>" to src/test.cpp

docker run --rm -ti -v ${PWD}:/home/conan/project conanio/gcc10-ubuntu18.04
sudo pip install --upgrade conan==1.59.0
cd project

conan create . --profile:build .conan/profiles/gcc10 --profile:host .conan/profiles/gcc10 --build missing  -c tools.system.package_manager:mode=install -c tools.system.package_manager:sudo=True
```

works as expected.

## Test with conan 2.0.0

```
conan new -d name=boost_test -d version=0.0.1 cmake_lib
#Add glog to requirement
#Add "#include <glog/logging.h>" to src/test.cpp

docker run --rm -ti -v ${PWD}:/home/conan/project conanio/gcc10-ubuntu18.04
sudo pip install --upgrade conan==2.0.0
cd project

conan create . --profile:build .conan/profiles/gcc10 --profile:host .conan/profiles/gcc10 --build missing  -c tools.system.package_manager:mode=install -c tools.system.package_manager:sudo=True
```

produces following error:

```
test/0.0.1: Running CMake.build()
test/0.0.1: RUN: cmake --build "/home/conan/.conan2/p/t/test40f3ed19ff62f/b/build/Release" -- -j2
Scanning dependencies of target test
[ 50%] Building CXX object CMakeFiles/test.dir/src/test.cpp.o
In file included from /home/conan/.conan2/p/t/test40f3ed19ff62f/b/src/test.cpp:3:
/home/conan/.conan2/p/glogb51c26a03204b/p/include/glog/logging.h:89:10: fatal error: gflags/gflags.h: No such file or directory
   89 | #include <gflags/gflags.h>
      |          ^~~~~~~~~~~~~~~~~
compilation terminated.
CMakeFiles/test.dir/build.make:62: recipe for target 'CMakeFiles/test.dir/src/test.cpp.o' failed
make[2]: *** [CMakeFiles/test.dir/src/test.cpp.o] Error 1
CMakeFiles/Makefile2:75: recipe for target 'CMakeFiles/test.dir/all' failed
make[1]: *** [CMakeFiles/test.dir/all] Error 2
Makefile:129: recipe for target 'all' failed
make: *** [all] Error 2

test/0.0.1: ERROR: 
Package 'b8d23f4b22d977224e6aa923066bfc1cbbfc9c15' build failed
test/0.0.1: WARN: Build folder /home/conan/.conan2/p/t/test40f3ed19ff62f/b/build/Release
*********************************************************
Recipe 'test/0.0.1' cannot build its binary
It is possible that this recipe is not Conan 2.0 ready
If the recipe comes from ConanCenter check: https://conan.io/cci-v2.html
If it is your recipe, check it is updated to 2.0
*********************************************************

ERROR: test/0.0.1: Error in build() method, line 47
        cmake.build()
        ConanException: Error 2 while executing
```
