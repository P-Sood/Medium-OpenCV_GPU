# Installing OpenCV-Python from Source
### Compile openCV with GPU support to speed up operations


This guide will walk you through the process of installing OpenCV-Python from the source. Before beginning, make sure to remove any existing OpenCV-Python directories and load the necessary modules:

Step 0:
    Have cuda and cudnn installed properly on your environment: 
    https://medium.com/geekculture/install-cuda-and-cudnn-on-windows-linux-52d1501a8805#68ce

Next, clone the OpenCV-Python repository and navigate to the newly created directory:

Step 1:

    git clone --recursive https://github.com/opencv/opencv-python.git
Step 2:

    cd opencv-python

Once inside the OpenCV-Python directory, check out the stable version of the code that you wish to install. As of today, the stable version is 4.7.0.72, which corresponds to commit f9de34ec8bc8bc5d61e5e35c0721676993da7d71. Note that if you attempt to build the latest version, you may encounter a PEP 440 error.

Step 3:

    git checkout $STABLE_VERSION
    git checkout f9de34ec8bc8bc5d61e5e35c0721676993da7d71

Now it's time to set up your build environment by exporting the necessary CMake arguments:

Step 4:

    export CMAKE_ARGS="-DOPENCV_EXTRA_MODULES_PATH=/home/prsood/projects/def-whkchun/prsood/opencv-python/opencv_contrib/modules -DWITH_LAPACK=OFF -DENABLE_FAST_MATH=1 -DCUDA_FAST_MATH=1 -DBUILD_SHARED_LIBS=OFF -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF -DBUILD_EXAMPLES=OFF -DWITH_OPENEXR=OFF -DWITH_CUDA=ON -DWITH_CUBLAS=ON -DWITH_CUDNN=ON -DOPENCV_DNN_CUDA=ON -DCUDA_GENERATION=Volta -DENABLE_PRECOMPILED_HEADERS=OFF /home/prsood/projects/def-whkchun/prsood/opencv-python"

Let's go through each of these arguments one by one to understand what they do:

- `-DOPENCV_EXTRA_MODULES_PATH`: This option specifies a semicolon-separated list of directories containing extra modules that will be added to the build.
- `-DWITH_LAPACK=OFF`: Keeping this flag on may cause errors in conjunction with the imlk library, which is Intel's version of GCC. 
                       This flag disables the use of LAPACK (Linear Algebra PACKage) library. 
- `-DENABLE_FAST_MATH=1`: This flag enables the use of fast math operations.
- `-DCUDA_FAST_MATH=1`: This flag enables the use of fast math operations with CUDA.
- `-DBUILD_SHARED_LIBS=OFF`: This flag disables building shared libraries and builds static libraries instead.
- `-DBUILD_TESTS=OFF`: This flag disables building tests.
- `-DBUILD_PERF_TESTS=OFF`: This flag disables building performance tests.
- `-DBUILD_EXAMPLES=OFF`: This flag disables building examples.
- `-DWITH_OPENEXR=OFF`: This flag disables the use of OpenEXR library.
- `-DWITH_CUDA=ON`: This flag enables CUDA support.
- `-DWITH_CUBLAS=ON`: This flag enables CUDA Basic Linear Algebra Subprograms (cuBLAS) support.
- `-DWITH_CUDNN=ON`: This flag enables CUDA Deep Neural Network (cuDNN) support.
- `-DOPENCV_DNN_CUDA=ON`: This flag enables CUDA support for OpenCV’s Deep Neural Network module.
- `-DCUDA_GENERATION=Volta`: This flag specifies the target CUDA architecture generation (in this case, Volta).
- `-DENABLE_PRECOMPILED_HEADERS=OFF`: This flag disables the use of precompiled headers.

After setting up your build environment, enable contrib by exporting the `ENABLE_CONTRIB` variable:

Step 5:

    export ENABLE_CONTRIB=1

Now you're ready to build OpenCV-Python by running `pip wheel .` with the `--verbose` flag:

Step 6:

    pip wheel . --verbose


Once the build process is complete, you should have a new wheel file in your current directory. Simply install this wheel using `pip install` and you're done!

Step 7:

    pip install $*.whl$
    pip install opencv_contrib_python-4.7.0.72-cp37-cp37m-linux_x86_64.whl

mine was opencv_contrib_python-4.7.0.72-cp37-cp37m-linux_x86_64.whl


Thank you for reading my first article on Medium!
