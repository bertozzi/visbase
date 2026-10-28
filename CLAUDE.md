# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **Computer Vision course repository** (University of Parma) containing lecture slides and C++/OpenCV lab exercises. The repository is managed with Google's `repo` tool — the actual source lives across several git subprojects, wired together by `.repo/manifests/default.xml`:

- `.` (base) — `visbase.git`
- `lab/` — `vislabs.git`
- `slides/` — `visslides.git`
- `slidespdf/` — `visslidespdf.git`

Each academic year is a separate branch (`2023`, `2024`, `2026`, ...) checked out across all four subprojects at once. To sync/switch year:

```bash
repo sync
repo forall -c 'git checkout <year>'
```

The current checkout is on branch `2026`.

## Build System

Each lab exercise is a self-contained CMake project. Standard build flow:

```bash
cd lab/<exercise>/
mkdir build && cd build
cmake ..
make
```

Key CMake conventions used across labs:
- `cmake_minimum_required(VERSION 2.8)`
- `find_package(OpenCV REQUIRED)` (a couple of labs pin `OpenCV 3.4.3`)
- Flags: `-std=c++11 -Wall -g`
- Executables link against `${OpenCV_LIBS}`; some labs (e.g. `L05-inverse`) also use Eigen (`eigen3/Eigen/...`)
- The executable target name doesn't always match the directory/topic name (e.g. `lab/L08`'s target is `ransac`, built from `skel.cpp`)
- `lab/.gitignore` ignores `build/`, so it's safe to build in-place inside each lab directory

## Lab Structure

Labs live in `lab/`. For topics with a skeleton/solution split, the student starting point is `L0X-topic/` and the solved version is the sibling directory `L0X-topic-solved/` (not a `sol/` subdirectory). A matching instruction PDF (`L0X-topic.pdf`) usually sits next to both. Some labs (e.g. `L01-data`) ship only test images/data in the skeleton, with no starter `.cpp`.

| Lab | Topic |
|-----|-------|
| L01-data | Bayer patterns, image channels, pixel formats |
| L02-convolution | 2D convolution, Sobel filtering |
| L03-background-sub | Frame differencing, background subtraction |
| L04-morphology | Morphological operations |
| L05-edges | Sobel, Canny edge detection |
| L05-inverse | Inverse projection using camera params (OpenCV + Eigen) |
| L06-pinhole | Pinhole camera model, projection |
| L07-stereo | Stereo vision, epipolar geometry, 3D reconstruction |
| L08 | RANSAC, Hough transform, model fitting |
| L10-kmeans (also standalone `k-means`) | K-means image segmentation |
| SIFT | Scale-Invariant Feature Transform (C++) |
| MBDA / esercitazione_MBDA | Multi-Band Diffusion Analysis, incl. a standalone k-means exercise handout |
| antares, simple | Minimal/reference OpenCV project skeletons |

## Code Conventions

All source files are **C++11** with OpenCV. Common patterns:
- Image data: `cv::Mat`
- Core headers: `opencv2/core/core.hpp`, `opencv2/highgui/highgui.hpp`, `opencv2/imgproc/imgproc.hpp`
- Image I/O: `cv::imread()` / `cv::imshow()`
- CLI parsing: `getopt()` or `cv::CommandLineParser`
- Interactive windows with keyboard event loops (`cv::waitKey()`)

## Slides

Lecture slides are in LibreOffice Impress `.odp` format in `slides/`, with PDF exports in `slidespdf/`. Topics run from `00_intro` through `20_CNN`. Only `.odp` files are tracked in git (PDFs are gitignored).
