# USGS ASP Scripts #
This Git repository consolidates a collection of Bash scripts that have been developed as part of a highly-automated workflow for generating digital terrain models (DTMs) from CTX and HiRISE stereo image data using the NASA Ames Stereo Pipeline (ASP).

This repository was manually forked from the UChicago ASP Scripts project, hosted at the University of Chicago: https://psd-repo.uchicago.edu/kite-lab/uchicago_asp_scripts

Most of these Bash scripts are wrappers for the various USGS ISIS3 and ASP binaries used to generate DTMs from stereo image data. These scripts were developed to be run in a high-performance computing environment using the SLURM job manager. As such, many of the scripts contain calls to *scontrol* in order to generate a file containing a list of compute nodes for *parallel_stereo* to use. See the comments in individual Bash scripts for details on modifying them for use with another job manager (i.e. PBS) or for use on a single machine.

## Dependencies ##
- USGS ISIS3 <http://isis.astrogeology.usgs.gov/>
- NASA Ames Stereo Pipeline <https://ti.arc.nasa.gov/tech/asr/intelligent-robotics/ngt/stereo/>
- GDAL <http://www.gdal.org/>
- GNU Parallel <https://www.gnu.org/software/parallel/>
- pedr2tab <http://pds-geosciences.wustl.edu/missions/mgs/molasoftware.html#PEDR2TAB>
-- At USGS, we use a USGS-modified version that works on most modern flavors of Linux, and Mac OS X <https://github.com/USGS-Astrogeology/socet_set/blob/master/SS4HiRISE/Software/ISIS3_MACHINE/SOURCE_CODE/pedr2tab.PCLINUX.f>

## Supported Platforms ##
These scripts have been developed and tested on recent versions of Fedora, Ubuntu and Scientific Linux. They should work on other flavors of GNU/Linux either natively or in a VM.
I expect some of the scripts will fail on Mac OS X because the versions of *sed* and *awk* that ship with OS X tend to be older and have different functionality compared to their GNU cousins. A workaround would be to compile GNU versions of these programs from source or install from a package manager like MacPorts or Homebrew.

## Basic Usage ##
Scripts for processing CTX and HiRISE data are organized into their own subdirectories.  The order in which individual scripts should be run is listed below. Please see comments in the individual scripts for detailed usage information.  Running any of the scripts without arguments will print a usage message.

### CTX ###
1. ctxedr2lev1eo.sh
2. asp_ctx_lev1eo2dem.sh
3. asp_ctx_step2_map2dem.sh
4. pedr_bin4_pc_align.sh
5. (Estimate max displacement between initial CTX DTM and MOLA PEDR using your favorite GIS software)
6. asp_ctx_map_ba_pc_align2dem.sh

### HiRISE ###
1. asp_hirise_prep.sh
2. asp_hirise_map2dem.sh
3. (Estimate max displacement between initial HiRISE DTM and reference DTM, such as CTX, using your favorite GIS)
4. asp_hirise_pc_align2dem.sh

## Referencing This Workflow ##
Please cite one or both of the following LPSC abstracts in any publications that make use of this work or derivatives thereof:
1. Mayer, D.P. and Kite, E.S., "An Integrated Workflow for Producing Digital Terrain Models of Mars from CTX and HiRISE Stereo Data Using the NASA Ames Stereo Pipeline," (2016) LPSC XLVII, Abstr. #1241. <https://www.hou.usra.edu/meetings/lpsc2016/pdf/1241.pdf>
E-poster: <https://www.lpi.usra.edu/meetings/lpsc2016/eposter/1241.pdf>
2. Mayer, D. P., "An Improved Workflow for Producing Digital Terrain Models of Mars from CTX Stereo Data Using the NASA Ames Stereo Pipeline," (2018) LPSC XLIX, Abstr. #1604. <https://www.hou.usra.edu/meetings/lpsc2018/pdf/1604.pdf>
E-poster: <https://www.hou.usra.edu/meetings/lpsc2018/eposter/1604.pdf>


The Ames Stereo Pipeline itself should be cited according to guidelines outlined in the official ASP documentation.
