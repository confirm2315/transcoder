# Golang Transcoding Library

<br />

<div align="center">
  <!-- Build status -->
  <a href="https://circleci.com/gh/floostack/transcoder">
    <img src="https://circleci.com/gh/floostack/transcoder.svg?style=svg" alt="Build Status" />
  </a>

  <!-- Code Quality -->
  <a href="https://www.codacy.com/manual/floostack/transcoder?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=floostack/transcoder&amp;utm_campaign=Badge_Grade">
    <img src="https://app.codacy.com/project/badge/Grade/f8ee19ef723b4134bb8bb1f9c439959e" alt="Build Status" />
  </a>

</div>

<br />

<div align="center">
  <sub>Created by <a href="https://floostack.com">FlooStack</a>.</sub>
</div>

## Features

<dl>
  <dt>Ease use</dt>
  <dd>Implement your own business logic around easy interfaces</dd>

  <dt>Transcoding progress</dt>
  <dd>Obtain progress events generated by transcoding application process</dd>
</dl>

## Download from Github

```shell
go get github.com/floostack/transcoder
```

## Example

```go
package main

import (
	"log"

	ffmpeg "github.com/floostack/transcoder/ffmpeg"
)

func main() {

	format := "mp4"
	overwrite := true

	opts := ffmpeg.Options{
		OutputFormat: &format,
		Overwrite:    &overwrite,
	}

	ffmpegConf := &ffmpeg.Config{
		FfmpegBinPath:   "/usr/local/bin/ffmpeg",
		FfprobeBinPath:  "/usr/local/bin/ffprobe",
		ProgressEnabled: true,
	}

	progress, err := ffmpeg.
		New(ffmpegConf).
		Input("/tmp/avi").
		Output("/tmp/mp4").
		WithOptions(opts).
		Start(opts)

	if err != nil {
		log.Fatal(err)
	}

	for msg := range progress {
		log.Printf("%+v", msg)
	}
}
```
