# Deinterlace Studio

Deinterlace Studio is a quality-first Windows application designed to make
high-quality video deinterlacing as easy as possible. Instead of requiring the
user to learn and tune the large number of parameters exposed by many advanced
deinterlacing tools, the default **Automatic** route analyzes the source and
chooses the highest-quality appropriate settings for you.

The goal is simple: select a video, let the app measure its field order and
interlace characteristics, and produce clean progressive output without having
to become an expert in QTGMC, BWDIF, field cadence, pixel formats, or encoder
parameters.

## Download

[Download DeinterlaceStudio.exe for Windows](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.6/DeinterlaceStudio.exe)

Deinterlace Studio is portable. Download `DeinterlaceStudio.exe` and run it
directly; no installer is required.

- Current release: **v1.14.6**
- SHA-256: `93ED9B5C7AE93760898532FE93D1FEF458C87B9198622025F1FA9CEBAA9D1426`
- Windows FileVersion/ProductVersion: **1.14.6**

The executable is currently unsigned, so Windows may display a SmartScreen
warning when it is first launched.

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
| **BWDIF CUDA** | The fastest option on supported NVIDIA hardware, but the app author's comparisons found noticeably lower output quality than QTGMC or BWDIF CPU. Speed is its main advantage, so compare representative clips before using it for important work. |

If you are unsure, use **Automatic**. It follows the app's quality-first policy
and applies hardware acceleration only where applicable to the selected safe
path.

Before committing a large collection to BWDIF CUDA—or whenever the difference
between backends matters—compare short outputs side by side with
[SKV89's Video Compare Tool](https://github.com/skv89/SKV89s-Video-Compare-Tool).
Different footage can expose different weaknesses, so a representative sample
is more useful than judging speed alone.

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
when the lower temporal cadence or smaller output is intentional.

Recovering both original field-time samples is a deinterlacing function, not a
feature of Topaz's denoisers themselves. Topaz documents its denoise model as a
separate task-specific filter, while its Dione interlaced workflow is the stage
that doubles frame rate. Once an interlaced source has already been reduced to
25p, a downstream denoiser cannot recover the discarded second field as genuine
source evidence; later frame interpolation can only synthesize a replacement.
See Topaz's documentation for its
[denoise filter](https://docs.topazlabs.com/topaz-video/filters/denoise) and
[Dione deinterlacing workflow](https://docs.topazlabs.com/video-ai/how-to-guide/restore-and-upscale-noisy-footage).

Where the downstream workflow accepts the rate, supplying 50p rather than 25p
gives diffusion-based generative restoration models such as SEEDVR2 and Topaz
Starlight Precise (SLP) twice as many genuine temporal samples from which to
understand motion. That added temporal context can improve motion continuity
and reduce the likelihood of the smearing and ghosting commonly noticed in
fast-moving scenes. It cannot guarantee that a generative model will never
produce those artifacts, but it gives the model more real motion evidence than
a half-rate input. Topaz identifies the
[Starlight family](https://docs.topazlabs.com/topaz-video/project-starlight-series)
as diffusion-based.

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

- Measured field-order and interlace analysis
- Quality-first VapourSynth QTGMC processing and FFmpeg BWDIF alternatives
- Validated repair workflow for damaged sources before QTGMC processing
- Ordered batch processing with per-file preflight checks
- Optional temporal denoising in the same job
- Mathematically lossless FFV1 archival output with source-matched precision
- Preservation of compatible audio, subtitle, attachment, chapter, and metadata tracks
