# Streams-MediaStreamTrack API Specification _:stars:_:movie_camera:

This is the repository for `stream-mediastreamtrack`, an experimental API for generating [`Streams`](https://streams.spec.whatwg.org/#stream) out of a [`MediaStreamTrack`](https://www.w3.org/TR/mediacapture-streams/#mediastreamtrack).

You're welcome to contribute! Let's make the Web rock our socks off!

## Introduction

[`Streams`](https://streams.spec.whatwg.org/#stream) are designed to provide real time streams of data with powerful semantics (e.g. built-in backpressure and queuing) to allow users to build higher-level abstractions.

[`MediaStreamTracks`](https://www.w3.org/TR/mediacapture-streams/#mediastreamtrack) are opaque handles to Real-Time video/audio being transported in the browser. To access this data, users must resort to contortions such as reflexion on intermediate HTML elements (e.g. `<canvas>`) or offline processing (e.g. using [`MediaRecorder`](https://w3c.github.io/mediacapture-record/MediaRecorder.html)).  These approaches, however, lose the timing information, introduce friction in the interoperability between platform entities and limit the possible data processing to whatever is offered by the platform.  This situation is made only more evident with the arrival of powerful programmable environments such as [WebAssembly](http://webassembly.org/) where users will naturally expect to be able to manipulate Real-Time media.

## Use cases

Every single use case that is not covered by the current array of `MediaStreamTrack` sources and sinks (see the diagram below) is a potential use case.

![MST](mediastreamtrack_sources_and_sinks.png)

Some random examples:

- Accessing Video/Audio being produced by a `<video>`/`<canvas>` and adding subtitles.
- Adjusting the presentation timestamp of the media to simulate a slow-motion or timelapse effect.
