# mongodb-docs
Automates doxygen document generation for mongodb

# Prerequisites
1. cmake
2. doxygen
3. graphviz

# Build documentation
```
$ cmake -B ./build && cd ./build && make
```
or just
```
./build.sh
```

# Documentation directory
./build/docs/html