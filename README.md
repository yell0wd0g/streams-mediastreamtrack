# Streams-MediaStreamTrack API Specification

This is the repository for `stream-mediastreamtrack`, an experimental API for generating [`Streams`](https://streams.spec.whatwg.org/#stream) out of a [`MediaStreamTrack`](https://www.w3.org/TR/mediacapture-streams/#mediastreamtrack).

You're welcome to contribute! Let's make the Web rock our socks off!

## Introduction

[`Streams`](https://streams.spec.whatwg.org/#stream) are designed to provide real time streams of data with powerful semantics (e.g. built-in backpressure and queuing) to allow users to build higher-level abstractions.

[`MediaStreamTracks`](https://www.w3.org/TR/mediacapture-streams/#mediastreamtrack) are opaque handles to Real-Time video/audio being transported in the browser. To access this data, users must resort to contortions such as reflexion on intermediate HTML elements (e.g. `<canvas>`) or offline processing (e.g. using [`MediaRecorder`](https://w3c.github.io/mediacapture-record/MediaRecorder.html)).  These approaches, however, lose the timing information, introduce friction in the interoperability between platform entities and limit the possible data processing to whatever is offered by the platform.


  This situation is made only more evident with the arrival of powerful programmable environments such as [WebAssembly](http://webassembly.org/) where users will naturally expect to be able to manipulate Real-Time media.



## Use cases

Every single use case that is not covered by the current array of `MediaStreamTrack` sources and sinks (see the diagram below) is a potential use case.

![MST](mediastreamtrack_sources_and_sinks.png)

Some random examples of use cases/actions that are enabled:

- Measuring the amount of Video Frames produced and/or calculating the source frame rate.
- Add subtitles to Video/Audio being produced by a `<video>`/`<canvas>` and adding subtitles.
- Adjusting the presentation timestamp of the media to simulate a slow-motion or timelapse effect.


## Current Related Efforts and Workarounds :wrench:

The most usual hack to access Video data is to cast a given `MediaStreamTrack` onto a `<video>` element and onto a `<canvas>` in turn that is subsequently read back -- `<video>` elements provide no `drawed` event so it's up to the user to blit from `<video>` to `<canvas>` on a timely basis.  Moreover, usually reading from `<canvas>` implies a costly read back from GPU.

Chrome [Pepper API](https://developer.chrome.com/native-client/pepper_dev) introduced and supports both [MediaStreamVideoTrack](https://developer.chrome.com/native-client/pepper_dev/cpp/classpp_1_1_media_stream_video_track) and [MediaStreamAudioTrack](https://developer.chrome.com/native-client/pepper_dev/cpp/classpp_1_1_media_stream_audio_track) addressing a similar situation as the one described here.

## Examples and demos

http://rawgit.com/yellowdoge/streams-mediastreamtrack/master/index.html#examples

## Notes on bikeshedding :bicyclist:

To compile, run:

```
curl https://api.csswg.org/bikeshed/ -F file=@index.bs -F force=1 > index.html
```

if the produced file has a strange size (i.e. zero), then something went terribly wrong; run instead

```
curl https://api.csswg.org/bikeshed/ -F file=@index.bs -F output=err
```
and try to figure out why `bikeshed` did not like the `.bs` :'(
