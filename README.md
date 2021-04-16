# mongodb-docs
Automates doxygen document generation for mongodb

# Prerequisites
1. cmake
2. doxygen
3. graphviz

# Build documentation
```
$ mkdir ./build
$ cd ./build && cmake .. && make
```
or just
```
./build.sh
```

# Documentation directory
start with ./build/docs/html/index.html

# Where to find MongoDB source
1. The environment variable $MONGODB_ROOT
2. ~/mongo
3. https://github.com/mongodb/mongo

# What are documented and what features are included
1. All public/protected/private members
2. All namespaces includig anonymous namespaces
3. C/C++ source code and *.md below following directories
   - mongo/src/mongo/base
   - mongo/src/mongo/bson
   - mongo/src/mongo/crypto
   - mongo/src/mongo/db
   - mongo/src/mongo/dbtests
   - mongo/src/mongo/embedded
   - mongo/src/mongo/executor
   - mongo/src/mongo/idl
   - mongo/src/mongo/logv2
   - mongo/src/mongo/platform
   - mongo/src/mongo/rpc
   - mongo/src/mongo/s
   - mongo/src/mongo/stdx
   - mongo/src/mongo/transport
   - mongo/src/mongo/unittest
   - mongo/src/mongo/util
4. *.md below mongo/docs
5. Source browser
6. Symbol & file search
7. Inheritance diagram & collaboration diagram
8. Include dependency diagram
9. Interactive diagram through SVG

# Supported platforms for build
1. Ubuntu 18.04
2. Homebrew on MacOS X Catalina
