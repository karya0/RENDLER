RENDLER implementation in C++
=============================

Dependencies:
============
- libboost\_regex.so
- libcurl.so
- Makefile assumes all 3rdparty libraries/headers to be available in the
  default include path (/usr/include?).
- render.js present in the parent directory.

Assumptions:
===========
- CPUs per task: 0.2
- Memory per task: 32 MB

Limitations/Features:
====================
- Doesn't store the images to S3, just locally.
- Image files are kept in rendler-work-dir in the same folder as the
  render\_executor executable.
- Images files are named R<N> where N is a monotonouly increasing integer.
- It wouldn't crawl outside of the given base URL (it will still render those
  webpages) to avoid pulling in too much data.
- Doesn't check for rendering error if a URL is not rendered.  Ideally, it
  should have a dummy image to indicate rendering failure.

Communication between Scheduler and Executors:
=============================================
- Each framework message consists of a vector of strings:
    - RenderExecuter->Scheduler:    { taskId, taskUrl, filepath }
    - CrawlExecuter->Scheduler:     { taskId, taskUrl, \<urls>+ }
