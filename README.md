# Deinterlace Studio

Deinterlace Studio is a quality-first Windows application designed to make
high-quality video deinterlacing as easy as possible. Instead of requiring the
user to learn and tune the large number of parameters exposed by many advanced
deinterlacing tools, the default **Automatic** route analyzes the source and
chooses the highest-quality appropriate settings for you.

The goal is simple: select a video, let the app measure its field order and
interlace characteristics, and produce clean progressive output without the user having
to become an expert in QTGMC, BWDIF, field cadence, pixel formats, or encoder
parameters.

## Download

[Download DeinterlaceStudio.exe for Windows](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.7/DeinterlaceStudio.exe)

Deinterlace Studio is portable. Download `DeinterlaceStudio.exe` and run it
directly; no installer is required.

- Current release: **v1.14.7**
- SHA-256: `528F20705F90BD0B58F45CF97768B0935847DD160929E34A52FE8980F9314C67`
- Windows FileVersion/ProductVersion: **1.14.7**

The executable is currently unsigned, so Windows may display a SmartScreen
warning when it is first launched.

## What is new in v1.14.7

- **One-click Start.** Add a video and click Start; automatic probing and interlace analysis run when needed. Unclear quick field-order samples trigger one thorough IDet scan, while unresolved results still stop for review. Damage checks and validated QTGMC repair remain separate safeguards; manual Probe is optional.
- **Maximized startup and improved layout.** The app opens maximized and restores safely after invalid or off-screen saved geometry. Queue, planning and dependency controls remain accessible on smaller screens.
- **Optional Vulkan setup and simpler decoding choices.** Install only the verified app-local NNEDI3VK add-on, without reinstalling the full processing runtime or changing system Python. Compatible GPUs must pass a real QTGMC render test. CPU QTGMC remains the default; Vulkan uses the existing FP32 quality settings. Hardware decode now offers Automatic and Off, independently of GPU deinterlacing.
- **Measured Vulkan guidance.** Hover help reports 11%-59% faster QTGMC frame processing in two 720x576 tests on a Ryzen 9 9950X3D and RTX PRO 6000 Blackwell. These figures exclude initialization and encoding. No obvious quality loss was seen in the inspected CPU/Vulkan still frames, but outputs are not pixel-identical and results vary by footage and hardware.
- **More robust dependencies and source handling.** Broken optional tools no longer prevent otherwise usable CPU paths, cancellation reaches capability/setup checks, and staged FFmpeg/FFprobe pairs are checked for compatibility. Full-range editing-master conversion, RGB precision and decoded-color validation are improved. Unsupported alpha/float, RGB without known colorimetry, and HDR DNxHR paths stop with an explanation.
- **Edit the waiting batch queue while processing.** Select any row to inspect its current settings. Use Remove/Delete to remove waiting rows, or drag them and use Move up/down to change the remaining order. The active row and already-started rows are protected until the batch finishes. Removing a queue row never deletes source, repair, or output files. Every retained row still completes preflight before encoding starts.
- **Clearer repair-copy names.** New repair-only copies use `.repair.mkv`, without QTGMC in the filename. These copies preserve interlacing and have not been deinterlaced. The final progressive output still uses `.QTGMC_deinterlaced` (or `.BWDIF_deinterlaced` for BWDIF). Existing files are not renamed.
- **Four clearer display-aspect choices.** Keep the original size and pixel shape; make square pixels with an exact aspect ratio and no downscaling; make square pixels while keeping source height and resizing width; or set a display ratio without resizing. The help distinguishes display ratios from resolution and labels example dimensions as examples.
- **Source-aware ProRes and DNxHR.** The app chooses an appropriate supported profile from each source's depth and chroma instead of always forcing the largest 4:4:4 profile. The selected profile and encoder settings remain visible; these editing codecs are still lossy, and conversion does not recover detail missing from the source.
- **Current selection and clearer help.** Both single-file and batch views show the source-to-output format, selected encoder and effective parameters. The reorganized layout keeps the analysis window usable and the Build / refresh plan and Dependency doctor controls accessible. Probe and Thorough full-file IDet scan have hover help explaining automatic analysis, optional manual checks, and the distinction between field-order scanning and damage repair.

## The recommended automatic route

For most users, leave the backend and related processing controls on their
default or **Automatic** settings. The app performs measured field-order and
interlace analysis, selects its quality-first processing path, and uses
compatible hardware acceleration where it can do so without compromising the
chosen quality path.

Automatic mode is the safest recommendation when the priority is maximum
quality with the least setup. Advanced choices remain available for users who
want to compare backends or target a particular workflow.

## QTGMC and BWDIF

Deinterlace Studio offers two principal deinterlacing approaches:

| Option | What it is best suited for |
| --- | --- |
| **QTGMC** | The quality-first choice. It uses temporal and motion-aware processing through VapourSynth and is generally regarded as the stronger deinterlacer, especially for difficult motion, fine edges, and challenging source material. It is also the slower option. |
| **BWDIF (CPU)** | FFmpeg's efficient software deinterlacer. It is much faster and can still produce excellent results. In the app author's own comparisons, its output and QTGMC output have often been visually indistinguishable on ordinary material, although QTGMC remains the safer quality-first choice. |
| **BWDIF CUDA** | The fastest option on supported NVIDIA hardware, but my own comparisons found noticeably lower output quality than QTGMC or BWDIF CPU. Speed is its main advantage with this option, so compare representative clips before using it for important work. |

If you are unsure, use **Automatic**. It follows the app's quality-first policy
and applies hardware acceleration only where applicable to the selected safe
path.

If you want to be certain of the quality before selecting an option for large projects or important work, compare short outputs side by side with
[SKV89's Video Compare Tool](https://github.com/skv89/SKV89s-Video-Compare-Tool).
Different footage can expose different weaknesses, so a representative sample is more useful than judging speed alone. You can also use this to compare the results from my Deinterlace Studio app with say Topaz Video's deinterlacers.

## Batch processing

Queue multiple videos, apply shared deinterlacing and output settings, and let
the app preflight every row before a long encode begins.

[![Deinterlace Studio batch-processing interface](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-batch-processing.png)](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-batch-processing.png)

## Preserve every temporal field

For genuinely interlaced footage, **Preserve every temporal field — field-rate
progressive output (same duration)** retains the motion information represented
by both fields. A 25-frame/s interlaced source contains 50 distinct temporal
fields per second; field-rate output reconstructs 50 full-height progressive
frames per second at the same playback duration instead of reducing the output
to 25 progressive frames per second.

This is the recommended choice when preparing high-quality input for temporal
enhancement workflows such as SEEDVR2 and SLP. Choose nominal-rate output only
when the lower temporal cadence or smaller output is intentional. Note 
Topaz's deinterlacers only preserve the nominal frame rate (e.g. 25p). Once an 
interlaced source has already been reduced to 25p, downstream processes cannot recover 
the discarded second field as genuine source evidence; later frame interpolation can only 
synthesize a replacement.

Where the downstream workflow accepts the rate, supplying 50p rather than 25p
gives diffusion-based generative restoration models such as SEEDVR2 and Topaz
Starlight Precise (SLP) twice as many genuine temporal samples from which to
understand motion. That added temporal context can improve motion continuity
and reduce the likelihood of the smearing and ghosting commonly noticed in
fast-moving scenes. It cannot guarantee that a generative model will never
produce those artifacts, but it gives the model more real motion evidence than
a half-rate input. 

[![Deinterlace Studio field-rate output selection](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-field-rate-output.png)](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-field-rate-output.png)

## Optional temporal denoising

The built-in denoiser follows the same simplicity-first philosophy: it provides
a small, approachable set of controls and can run in the same job after
deinterlacing. Denoising is optional and should be enabled only when the source
benefits from it.

If you want a live preview and more opportunity to see how denoising choices
affect your footage before processing the full video, use
[Video Denoise Studio](https://github.com/skv89/Video-Denoise-Studio).

## Additional highlights

- Automatically measure field-order and interlace analysis
- Quality-first VapourSynth QTGMC processing and FFmpeg BWDIF alternatives
- Validated repair workflow for damaged sources before QTGMC processing
- Ordered batch processing with per-file preflight checks
- Optional temporal denoising in the same job
- Mathematically lossless FFV1 archival output with source-matched precision
- Preservation of compatible audio, subtitle, attachment, chapter, and metadata tracks
