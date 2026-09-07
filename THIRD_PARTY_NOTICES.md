# Deinterlace Studio — Third-Party Notices

Deinterlace Studio 1.14.7 includes TkinterDnD2 0.6.2 and its bundled TkDND
native extension for Explorer drag-and-drop.

The executable includes the Python/Tk runtime needed for its GUI. It does not
bundle FFmpeg, VapourSynth, the separate processing Python installation,
VSJetpack, or the optional NVIDIA denoiser packages. With the user's explicit consent, the
app-local dependency installer may download them into a separate managed
runtime beside the application without modifying system PATH, registry, Python,
or existing installations. Their source and license notices are presented in
the installer and recorded below for clarity.

## Optional app-local dependencies (not bundled)

- Gyan FFmpeg full build: GPLv3; FFmpeg components retain their respective
  upstream licenses.
- VapourSynth portable release: LGPL-2.1-or-later.
- Python embedded distribution: Python Software Foundation License.
- VSJetpack and its Python packages: MIT, with individual native plugins under
  their own upstream licenses.
- VapourSynth-nnedi3vk: GPL-3.0; optional Vulkan 1.4 NNEDI3 interpolation
  plugin resolved from its official PyPI Windows wheel. Vulkan-only setup pins
  version 1.0 / SHA-256 `290c8845dead5b24a46db7f8d77ba1375359e578ca0ac177b94829895a063b30`,
  retains the upstream license alongside the DLL/weights, and activates a
  separate app-local add-on only after a real FP32 QTGMC graph succeeds.
  Source and license: https://github.com/HolyWu/VapourSynth-nnedi3vk.
- VapourSynth-BM3DCUDA: GPL-2.0-or-later.
- VapourSynth-DFTTest2 CPU and optional NVIDIA NVRTC/cuFFT implementations:
  GPL-3.0; the app-local installer requests the NVRTC wheel and retains it only
  when the exact production graph passes.
- VapourSynth-vszipcu: MIT.
- NVIDIA CUDA NVRTC runtime installed as a dependency of GPU denoisers: NVIDIA
  proprietary license.

## TkinterDnD2

MIT License

Copyright (c) 2020 Philippe Gagné

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## TkDND

This software is copyrighted by:

Georgios Petasis, Athens, Greece.

e-mail: petasisg@yahoo.gr, petasis@iit.demokritos.gr

Mac portions (c) 2009-2014 Kevin Walzer/WordTech Communications LLC,
kw@codebykevin.com

The following terms apply to all files associated with the software unless
explicitly disclaimed in individual files.

The authors hereby grant permission to use, copy, modify, distribute, and
license this software and its documentation for any purpose, provided that
existing copyright notices are retained in all copies and that this notice is
included verbatim in any distributions. No written agreement, license, or
royalty fee is required for any of the authorized uses.

Modifications to this software may be copyrighted by their authors and need
not follow the licensing terms described here, provided that the new terms are
clearly indicated on the first page of each file where they apply.

IN NO EVENT SHALL THE AUTHORS OR DISTRIBUTORS BE LIABLE TO ANY PARTY FOR
DIRECT, INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES ARISING OUT OF
THE USE OF THIS SOFTWARE, ITS DOCUMENTATION, OR ANY DERIVATIVES THEREOF, EVEN
IF THE AUTHORS HAVE BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

THE AUTHORS AND DISTRIBUTORS SPECIFICALLY DISCLAIM ANY WARRANTIES, INCLUDING,
BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE, AND NON-INFRINGEMENT. THIS SOFTWARE IS PROVIDED ON AN "AS
IS" BASIS, AND THE AUTHORS AND DISTRIBUTORS HAVE NO OBLIGATION TO PROVIDE
MAINTENANCE, SUPPORT, UPDATES, ENHANCEMENTS, OR MODIFICATIONS.

GOVERNMENT USE: If you are acquiring this software on behalf of the U.S.
government, the Government shall have only "Restricted Rights" in the software
and related documentation as defined in the Federal Acquisition Regulations
(FARs) in Clause 52.227.19 (c) (2). If you are acquiring the software on behalf
of the Department of Defense, the software shall be classified as "Commercial
Computer Software" and the Government shall have only "Restricted Rights" as
defined in Clause 252.227-7013 (c) (1) of DFARs. Notwithstanding the foregoing,
the authors grant the U.S. Government and others acting in its behalf
permission to use and distribute the software in accordance with the terms
specified in this license.
