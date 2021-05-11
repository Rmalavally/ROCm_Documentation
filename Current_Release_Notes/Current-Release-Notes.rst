.. image:: /Current_Release_Notes/amdblack.jpg
|


=====================================
AMD ROCm™ Release Notes v4.2
=====================================
May, 2021

This page describes the features, fixed issues, and information about downloading and installing the ROCm software. It also covers known issues in the ROCm v4.2.0 release.

`Download AMD ROCm Release Notes PDF <https://github.com/RadeonOpenCompute/ROCm>`__


List of Supported Operating Systems
-----------------------------------

The AMD ROCm platform is designed to support the following operating systems:

-  Ubuntu 20.04.2 HWE (5.4 and 5.6-oem) and 18.04.5 (Kernel 5.4)

-  CentOS 7.9 (3.10.0-1127) & RHEL 7.9 (3.10.0-1160.6.1.el7) (Using devtoolset-7 runtime support)
   
-  CentOS 8.3 (4.18.0-193.el8)and RHEL 8.3 (4.18.0-193.1.1.el8) (devtoolset is not required)

-  SLES 15 SP2




Fresh Installation of AMD ROCm v4.2 Recommended
-----------------------------------------------

Complete uninstallation of previous ROCm versions is required before installing a new version of ROCm. An upgrade from previous releases to
AMD ROCm v4.2 is not supported. 

For more information, refer to the AMD ROCm Installation Guide at:

https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html

.. note::

   AMD ROCm release v3.3 or prior releases are not fully compatible with AMD ROCm v3.5 and higher versions. You must perform a fresh ROCm installation if you want to upgrade from AMD ROCm v3.3 or older to 3.5 or higher versions and vice-versa.
   
.. note::

   *render group* is required only for Ubuntu v20.04. For all other ROCm supported operating systems, continue to use *video group*.
   

-  For ROCm v3.5 and releases thereafter,the *clinfo* path is changed to
   - */opt/rocm/opencl/bin/clinfo*.

-  For ROCm v3.3 and older releases, the *clinfo* path remains unchanged
   - */opt/rocm/opencl/bin/x86_64/clinfo*.
   
   
.. note::

After an operating system upgrade, AMD ROCm may upgrade automatically and result in an error. This is because AMD ROCm does not support upgrades currently. You must uninstall and reinstall AMD ROCm after an operating system upgrade.

   
ROCm Multi Version Installation Update
---------------------------------------

With the AMD ROCm v4.2 release, the following ROCm multi-version installation changes apply:

The meta packages rocm-dkms are now deprecated for multi-version ROCm installs. For example, rocm-dkms3.8.0, rocm-dkms3.9.0.

-   Multi-version installation of ROCm should be performed by installing rocm-dev using each of the desired ROCm versions. For example, rocm-dev3.7.0, rocm-dev3.8.0, rocm-dev3.9.0.

-  The rock-dkms loadable kernel modules should be installed using a single rock-dkms package.

- ROCm v3.9 and above will not set any *ldconfig* entries for ROCm libraries for multi-version installation.  Users must set *LD_LIBRARY_PATH* to load the ROCm library version of choice.

.. note::

   The single version installation of the ROCm stack remains the same. The rocm-dkms package can be used for single version installs and is not deprecated at this time.



AMD ROCm Documentation Updates
-----------------------------------

ROCm Installation Guide
===========================

The AMD ROCm Installation Guide in this release includes:

-  Updated Supported Environments

-  Installation Instructions

-  HIP Installation Instructions


https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html


HIP Documentation Updates
===========================

-  HIP Programming Guide v4.2

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD%20HIP%20Programming%20Guide_v4.2.pdf


-  HIP API Guide v4.2

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD_HIP_API_Guide_4.2.pdf

-  HIP-Supported CUDA API Reference Guide v4.2

https://github.com/RadeonOpenCompute/ROCm/blob/master/HIP_Supported_CUDA_API_Reference_Guide_v4.2.pdf

-  HIP FAQ

   For more information, refer to

https://rocmdocs.amd.com/en/latest/Programming_Guides/HIP-FAQ.html#hip-faq


ROCm Data Center User and API Guide
====================================

-  ROCm Data Center Tool User Guide

   -  Reliability, Accessibility, and Serviceability (RAS) Plugin Integration

For more information, refer to the ROCm Data Center User Guide at,

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD_ROCm_DataCenter_Tool_User_Guide_v4.2.pdf

-  ROCm Data Center Tool API Guide

For more information, refer to the ROCm Data Center API Guide at,

https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_Data_Center_Tool_API_Guide_v4.2.pdf

   
ROCm SMI API Documentation Updates
===================================
   
-  ROCm SMI API Guide

For more information, refer to the ROCm SMI API Guide at,

https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_SMI_Manual_4.2.pdf

   

ROC Debugger User and API Guide 
===================================

-  ROC Debugger User Guide
   https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_Debugger_User_Guide_v4.2.pdf

-  Debugger API Guide
   https://github.com/RadeonOpenCompute/ROCm/blob/master/ROCm_Debugger_API_Guide_v4.2.pdf


General AMD ROCm Documentation Links
------------------------------------

Access the following links for more information:

-  For AMD ROCm documentation, see

   https://rocmdocs.amd.com/en/latest/

-  For installation instructions on supported platforms, see

   https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html

-  For AMD ROCm binary structure, see

   https://rocmdocs.amd.com/en/latest/Installation_Guide/Software-Stack-for-AMD-GPU.html

-  For AMD ROCm Release History, see

   https://rocmdocs.amd.com/en/latest/Current_Release_Notes/ROCm-Version-History.html
   
   


==============================================
What's New in This Release and Other Features
==============================================

HIP Enhancements 
-------------------

HIP Target Platform Macro
===========================

The platform macros are updated to target either the AMD or NVIDIA platform in HIP projects. They now include corresponding headers and
libraries for compilation/linking.

-  **HIP_PLATFORM_AMD** is defined if the HIP platform targets AMD. Note, **HIP_PLATFORM_HCC** was used previously if the HIP platform      targeted AMD. This is now deprecated.

-  **HIP_PLATFORM_NVIDIA** is defined if the HIP platform targets NVIDIA. Note, \_HIP_PLATFORM_NVCC_\_ was used previously if the HIP platform targeted NVIDIA. This is now deprecated.

For example,

::

            #if (defined(__HIP_PLATFORM_AMD__)) && !(defined(__HIP_PLATFORM_NVIDIA__))

            #include <hip/amd_detail/hip_complex.h>

            #elif !(defined(__HIP_PLATFORM_AMD__)) && (defined(__HIP_PLATFORM_NVIDIA__))

            #include <hip/nvidia_detail/hip_complex.h>

::

Updated HIP 'Include' Directories
==================================

In the ROCm v4.2 release, HIP *include* header directories for platforms are updated as follows:

-  *amd_detail/* - includes source header details for the 'amd' platform implementation. In previous releases, the 'hcc_detail' directory was
   defined, and it it is now deprecated.

-  *nvidia_detail/* - includes source header details for the 'nvidia' platform implementation. In previous releases, the 'nvcc_detail'
   directory was defined, and it is now deprecated.


HIP Stream Memory Operations
=============================

The ROCm v4.2 extends support to Stream Memory Operations to enable direct synchronization between Network Nodes and GPU. The following new
APIs are added:

-  hipStreamWaitValue32
-  hipStreamWaitValue64
-  hipStreamWriteValue32
-  hipStreamWriteValue64

For more details, see the HIP API guide at

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD_HIP_API_Guide_4.2.pdf


HIP Events in Kernel Dispatch
===============================

HIP events in kernel dispatch using *hipExtLaunchKernelGGL/hipExtLaunchKernel* and passed in the API are not 
explicitly recorded and should only be used to get elapsed time for that specific launch.

Events used across multiple dispatches, for example, start and stop events from different *hipExtLaunchKernelGGL/hipExtLaunchKernel* calls,
are treated as invalid unrecorded events. In such scenarios, HIP will display the error *â€œhipErrorInvalidHandleâ€* from *hipEventElapsedTime*.

For more details, refer to the HIP API Guide at

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD_HIP_API_Guide_4.2.pdf


Changed Environment Variables for HIP
======================================

In the ROCm v3.5 release, the Heterogeneous Compute Compiler (HCC) compiler was deprecated, and the HIP-Clang compiler was introduced for
compiling Heterogeneous-Compute Interface for Portability (HIP) programs. In addition, the HIP runtime API was implemented on top of
Radeon Open Compute Common Language Runtime (ROCclr). ROCclr is an abstraction layer that provides the ability to interact with different
runtime backends such as ROCr.

While the HIP_PLATFORM=hcc environment variable was functional in subsequent releases, in the ROCm v4.1 release, the following environment
variables were changed:

-  *HIP_PLATFORM=hcc to HIP_PLATFORM=amd*

-  *HIP_PLATFORM=nvcc to HIP_PLATFORM=nvidia*

Therefore, any applications continuing to use the *HIP_PLATFORM=hcc* variable will fail. You must update the environment variables to reflect
the changes as mentioned above.

       

ROCm Data Center Tool
---------------------

Grafana Integration
====================

The ROCm Data Center (RDC) Tool is enhanced with the Grafana plugin. Grafana is a common monitoring stack used for storing and visualizing
time series data. Prometheus acts as the storage backend, and Grafana is used as the interface for analysis and visualization. Grafana has a
plethora of visualization options and can be integrated with Prometheus for the ROCm Data Center (RDC) dashboard.

For more information about Grafana integration and installation, refer to the ROCm Data Center Tool User guide at:

https://github.com/RadeonOpenCompute/ROCm/blob/master/AMD_ROCm_DataCenter_Tool_User_Guide_v4.1.pdf


ROCm Math and Communication Libraries
-------------------------------------

rocSPARSE
===========

rocSPARSE extends support for:

-  gebsrmm
-  gebsrmv
-  gebsrsv
-  coo2dense and dense2coo
-  generic API including axpby, gather, scatter, rot, spvv, spmv, spgemm, sparsetodense, densetosparse
-  mixed indexing types in matrix formats

For more information, see

https://rocsparse.readthedocs.io/en/latest/

rocSOLVER
===========

rocSOLVER extends support for:

-  Eigensolver routines for symmetric/hermitian matrices:

   -  STERF, STEQR

-  Linear solvers for general non-square systems:

   -  GELS (API added with batched and strided_batched versions. Only the overdetermined non-transpose case is implemented in this
      release. Other cases will return rocblas_status_not_implemented status for now.)

-  Extended test coverage for functions returning information

-  Changelog file

-  Tridiagonalization routines for symmetric and hermitian matrices:

   -  LATRD
   -  SYTD2, SYTRD (with batched and strided_batched versions)
   -  HETD2, HETRD (with batched and strided_batched versions)

-  Sample code and unit test for unified memory model/Heterogeneous Memory Management (HMM)

For more information, see

https://rocsolver.readthedocs.io/en/latest/

hipCUB
=========

The new iterator DiscardOutputIterator in hipCUB represents a special kind of pointer that ignores values written to it upon dereference. It
is useful for ignoring the output of certain algorithms without wasting memory capacity or bandwidth. DiscardOutputIterator may also be used to
count the size of an algorithm's output, which was not known previously.

For more information, see

https://hipcub.readthedocs.io/en/latest/


HIP Enhancements
----------------

Support for hipEventDisableTiming Flag
=======================================

HIP now supports the hipEventDisableTiming flag for hipEventCreateWithFlags. Note, events created with this flag do not
record profiling data and provide optimal performance when used for synchronization.

Cooperative Group Functions
===============================

Cooperative Groups defines, synchronizes, and communicates between groups of threads and blocks for efficiency and ease of management. HIP
now supports the following kernel language Cooperative Groups types and functions:



.. image:: images/CGMain.PNG

   



Support for Extern Shared Declarations
========================================

Previously, it was required to declare dynamic shared memory using the HIP_DYNAMIC_SHARED macro for accuracy as using static shared memory in
the same kernel could result in overlapping memory ranges and data-races. Now, the HIP-Clang compiler provides support for extern
shared declarations, and the HIP_DYNAMIC_SHARED option is no longer required.

You may use the standard extern definition:

::

   extern __shared__ type var[];


OpenMP Enhancements and Fixes
-----------------------------

This release includes the following OpenMP changes:

-  Usability Enhancements
-  Fixes to Internal Clang Math Headers
-  OpenMP Defect Fixes

Usability Enhancements
========================

-  OMPD updates for flang
-  To support OpenMP debugging, the selected OpenMP runtime sources are
   included in lib-debug/src/openmp. The ROCgdb debugger will find these
   automatically.
-  Threadsafe hsa plugin for libomptarget
-  Support multiple devices with malloc and hostrpc
-  Improve hostrpc version check
-  Add max reduction offload feature to flang
-  Integration of changes to support HPC Toolkit
-  Support for fprintf
-  Initial support for GPU malloc and Free. The internal (device rtl) is
   required for GPU malloc and Free for nested parallelism.
   GPU malloc and Free are now replaced, which improves the device
   memory footprint.
-  Increase detail of debug printing controlled by
   LIBOMPTARGET_KERNEL_TRACE environment variable
-  Add support for -gpubnames in Flang Driver
-  Increase detail of debug printing controlled by
   LIBOMPTARGET_KERNEL_TRACE environment variable
-  Add support for -gpubnames in Flang Driver

Fixes to Internal Clang Math Headers
=========================================

This release includes a set of changes applied to Clang internal headers
to support OpenMP C, C++, FORTRAN, and HIP C. This establishes
consistency between NVPTX and AMDGCN offloading, and OpenMP, HIP, and
CUDA. OpenMP uses function variants and header overlays to define device
versions of functions. This causes Clang LLVM IR codegen to mangle names
of variants in both the definition and callsites of functions defined in
the internal Clang headers. The changes apply to headers found in the
installation subdirectory lib/clang/11.0.0/include.

The changes also temporarily eliminate the use of the libm bitcode
libraries for C and C++. Although math functions are now defined with
internal clang headers, a bitcode library of the C functions defined in
the headers is still built for the FORTRAN toolchain linking. This is
because FORTRAN cannot use C math headers. This bitcode library is
installed in lib/libdevice/libm-.bc. The source build of the bitcode
library is implemented with the aomp-extras repository and the
component-built script build_extras.sh.

OpenMP Defect Fixes
=======================
The following OpenMP defects are fixed in this release:

-  Openmpi configuration issue with real16.
-  [flang] The AOMP 11.7-1 Fortran compiler claims to support the
   -isystem flag, but ignores it.
-  [flang] producing internal compiler error when the character is used
   with KIND.
-  [flang] openmp map clause on complex allocatable expressions !$omp
   target data map( chunk%tiles(1)%field%density0).
-  Add a fatal error if missing -Xopenmp-target or -march options when
   -fopenmp-targets is specified. However, this requirement is not
   applicable for offloading to the host when there is only a single
   target and that target is the host.
-  Openmp error message output for no_rocm_device_lib was asserting.
-  Linkage on constant per-kernel symbols from external to
   weaklinkageonly to prevent duplicate symbols when building kokkos.
-  Add environment variables ROCM_LLD_ARGS ROCM_LINK_ARGS
   ROCM_SELECT_ARGS to test driver options without compiler rebuild.
-  Fix problems with device math functions being ambiguous, especially
   the pow function.ix aompcc to accept file type cxx.
-  Fix a latent race between host runtime and devicertl.

MIOpen Tensile Integration
--------------------------

MIOpenTensile provides host-callable interfaces to the Tensile library
and supports the HIP programming model. You may use the Tensile feature
in the HIP backend by setting the building environment variable value to
ON.

::

   MIOPEN_USE_MIOPENTENSILE=ON

MIOpenTensile is an open-source collaboration tool where external
entities can submit source pull requests (PRs) for updates.
MIOpenTensile maintainers review and approve the PRs using standard
open-source practices.

For more information about the sources and build system, see

https://github.com/ROCmSoftwarePlatform/MIOpenTensile




Known Issues
--------------

The following are the known issues in this release.

Upgrade to AMD ROCm v4.1 Not Supported
==========================================

An upgrade from previous releases to AMD ROCm v4.1 is not supported. A complete uninstallation of previous ROCm versions is required before
installing a new version of ROCm.

Performance Impact for Kernel Launch Bound Attribute
=========================================================

Kernels without the **launch_bounds** attribute assume the default maximum threads per block value. In the previous ROCm release, this
value was 256. In the ROCm v4.1 release, it is changed to 1024. The objective of this change ensures the actual threads per block value used
to launch a kernel, by default, are always within the launch bounds, thus, establishing the correctness of HIP programs.

**NOTE**: Using the above-mentioned approach may incur performance degradation in certain cases. Users must add a minimum launch bound to
each kernel, which covers all possible threads per block values used to launch that kernel for correctness and performance.

The recommended workaround to recover the performance is to add *“gpu-max-threads-per-block=256* to the compilation options for HIP
programs.

Issue with Passing a Subset of GPUs in a Multi-GPU System
============================================================

ROCm support for passing individual GPUs via the docker *--device* flag in a Docker run command has a known issue when passing a subset of GPUs in
a multi-GPU system. The command runs without any warning or error notification. However, all GPU executable run outputs are randomly
corrupted.

Using GPU targeting via the Docker command is not recommended for users of ROCm 4.1. There is no workaround for this issue currently.

Performance Impact for LDS-Bound Kernels
============================================

The compiler in ROCm v4.1 generates LDS load and stores instructions that incorrectly assume equal performance between aligned and misaligned
accesses. While this does not impact code correctness, it may result in sub-optimal performance.

This issue is under investigation, and there is no known workaround at this time.


Changed HIP Environment Variables in ROCm v4.1 Release
=======================================================

In the ROCm v3.5 release, the Heterogeneous Compute Compiler (HCC) compiler was deprecated, and the HIP-Clang compiler was introduced for compiling Heterogeneous-Compute Interface for Portability (HIP) programs. Also, the HIP runtime API was implemented on top of the Radeon Open Compute Common Language runtime (ROCclr). ROCclr is an abstraction layer that provides the ability to interact with different runtime backends such as ROCr. 

While the *HIP_PLATFORM=hcc* environment variable was functional in subsequent releases after ROCm v3.5, in the ROCm v4.1 release, changes to the following environment variables were implemented: 

* *HIP_PLATFORM=hcc was changed to HIP_PLATFORM=amd*

* *HIP_PLATFORM=nvcc was changed to HIP_PLATFORM=nvidia*

Therefore, any applications continuing to use the HIP_PLATFORM=hcc environment variable will fail.

**Workaround:**  Update the environment variables to reflect the changes mentioned above.



Deprecations
---------------

This section describes deprecations and removals in AMD ROCm.

Compiler Generated Code Object Version 2 Deprecation
======================================================

Compiler-generated code object version 2 is no longer supported and has been completely removed. Support for loading code object version 2 is
also deprecated with no announced removal release.

========================================
Driver Compability Issue in ROCm v4.1
========================================

In certain scenarios, the ROCm 4.1 run-time and userspace environment are not compatible with ROCm v4.0 and older driver implementations for 7nm-based (Vega 20) hardware (MI50 and MI60). 

To mitigate issues, the ROCm v4.1 or newer userspace prevents running older drivers for these GPUs.

Users are notified in the following scenarios:

* Bare Metal 
* Containers
 
Bare Metal
------------

In the bare-metal environment, the following error message displays in the console: 

*“HSA Error: Incompatible kernel and userspace, Vega 20 disabled. Upgrade amdgpu.”*

To test the compatibility, run the ROCm v4.1 version of rocminfo using the following instruction: 

*/opt/rocm-4.1.0/bin/rocminfo 2>&1 | less*

Containers
------------

A container (built with error detection for this issue) using a ROCm v4.1 or newer run-time is initiated to execute on an older kernel. The container fails to start and the following warning appears:

*Error: Incompatible ROCm environment. The Docker container requires the latest kernel driver to operate correctly. Upgrade the ROCm kernel to v4.1 or newer, or use a container tagged for v4.0.1 or older.*

To inspect the version of the installed kernel driver,  run either: 

* dpkg --status rock-dkms [Debian-based]

or

* rpm -ql rock-dkms [RHEL, SUSE, and others]

To install or update the driver, follow the installation instructions at:

https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html



===============
Deploying ROCm
===============

AMD hosts both Debian and RPM repositories for the ROCm v4.x packages.

For more information on ROCM installation on all platforms, see

https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html


DISCLAIMER 
============
The information contained herein is for informational purposes only, and is subject to change without notice. In addition, any stated support is planned and is also subject to change. While every precaution has been taken in the preparation of this document, it may contain technical inaccuracies, omissions and typographical errors, and AMD is under no obligation to update or otherwise correct this information. Advanced Micro Devices, Inc. makes no representations or warranties with respect to the accuracy or completeness of the contents of this document, and assumes no liability of any kind, including the implied warranties of noninfringement, merchantability or fitness for particular purposes, with respect to the operation or use of AMD hardware, software or other products described herein. No license, including implied or arising by estoppel, to any intellectual property rights is granted by this document. Terms and limitations applicable to the purchase or use of AMD’s products are as set forth in a signed agreement between the parties or in AMD's Standard Terms and Conditions of Sale.

* AMD®, the AMD Arrow logo, AMD Instinct™, Radeon™, ROCm® and combinations thereof are trademarks of Advanced Micro Devices, Inc. 

* Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.

* PCIe® is a registered trademark of PCI-SIG Corporation. Other product names used in this publication are for identification purposes only and may be trademarks of their respective companies.

