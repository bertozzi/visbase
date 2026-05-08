# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **Computer Vision course repository** (University of Parma, 2024) containing lecture slides and C++/OpenCV lab exercises. The repository is managed with Google's `repo` tool — the actual source lives across several git subprojects:

- `.` (base) — `visbase.git`
- `lab/` — `vislabs.git`
- `slides/` — `visslides.git`
- `slidespdf/` — `visslidespdf.git`

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
- `find_package(OpenCV REQUIRED)`
- Flags: `-std=c++11 -Wall -g`
- Executables link against `${OpenCV_LIBS}`

## Lab Structure

Labs are in `lab/` and numbered by topic. Each lab typically contains:
- A skeleton version (student starting point) in a subdirectory like `L0X-topic/`
- A solved version in `L0X-topic-sol/` or `L0X-topic/sol/`
- Test images (Lenna.png, domain-specific images)

| Lab | Topic |
|-----|-------|
| L01-data | Bayer patterns, image channels, pixel formats |
| L02-convolution | 2D convolution, Sobel filtering |
| L03-background-sub | Frame differencing, background subtraction |
| L04-morphology | Morphological operations |
| L05-edges | Sobel, Canny edge detection |
| L06-pinhole | Pinhole camera model, projection |
| L07-stereo | Stereo vision, epipolar geometry, 3D reconstruction |
| L08 | RANSAC, Hough transform, model fitting |
| L10-kmeans | K-means image segmentation |
| SIFT | Scale-Invariant Feature Transform (C++) |
| MBDA | Multi-Band Diffusion Analysis |

## Code Conventions

All source files are **C++11** with OpenCV. Common patterns:
- Image data: `cv::Mat`
- Core headers: `opencv2/core/core.hpp`, `opencv2/highgui/highgui.hpp`, `opencv2/imgproc/imgproc.hpp`
- Image I/O: `cv::imread()` / `cv::imshow()`
- CLI parsing: `getopt()` or `cv::CommandLineParser`
- Interactive windows with keyboard event loops (`cv::waitKey()`)

## Slides

Lecture slides are in LibreOffice Impress `.odp` format in `slides/`, with PDF exports in `slidespdf/`. Topics run from `00_intro` through `20_CNN`. Only `.odp` files are tracked in git (PDFs are gitignored).
