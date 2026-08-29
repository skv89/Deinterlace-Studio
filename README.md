# Deinterlace Studio

Deinterlace Studio is a quality-first Windows application for converting interlaced video into clean progressive output. It combines FFmpeg BWDIF and VapourSynth QTGMC processing with measured field-order analysis, validated source repair, optional temporal denoising, batch processing, and preservation-focused FFV1 output.

## Download

[Download the portable Windows executable](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.5/DeinterlaceStudio.exe)

The application is portable: download `DeinterlaceStudio.exe` and run it directly. The current public release is v1.14.5.

SHA-256: `B81065F41C95D861B6DAB0F86A70D34B7BB44724FE2C9A4AB6E62DC584E9856B`

## Highlights

- Automatic field-order and interlace analysis
- Quality-first VapourSynth QTGMC processing with FFmpeg BWDIF fallback
- Preserve-every-temporal-field output is the default for interlaced sources
- QTGMC runtime compatibility across supported VSJetpack API variants
- Validated repair of damaged sources before QTGMC processing
- Optional temporal denoising in the same job
- Ordered batch processing with per-file preflight checks
- Mathematically lossless FFV1 archival output with source-matched precision
- Preservation of compatible audio, subtitle, attachment, chapter, and metadata tracks

## Batch processing

Queue multiple videos, apply shared processing and output settings, and preflight every row before a long encode begins.

![Deinterlace Studio batch-processing interface](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-batch-processing.png)

## Preserve every temporal field

For genuinely interlaced footage, choose **Preserve every temporal field — field-rate progressive output (same duration)** when preparing a high-quality input for temporal enhancement workflows such as SEEDVR2 and SLP.

A 25-frame/s interlaced source contains 50 distinct temporal fields per second. Field-rate output reconstructs 50 full-height progressive frames per second while retaining the original playback duration, preserving the motion information carried by both fields. Nominal-rate output creates only 25 progressive frames per second and is best used when the lower temporal cadence or smaller output is intentional.

![Deinterlace Studio field-rate output selection](https://github.com/skv89/Deinterlace-Studio/releases/download/v1.14.3/deinterlace-studio-field-rate-output.png)
