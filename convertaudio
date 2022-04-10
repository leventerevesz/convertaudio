#!/bin/bash

if [ $# == 0 -o $1 == "-h" -o $1 == "--help" ]
then 
    echo "Converts the audio stream of a film to AAC format."
    echo "Creates a copy next to the original file. Only works with .mkv files."
    echo ""
    echo "Usage: $0 FILENAME [AUDIO_STREAM_NO]"
    exit 0
fi

filename=$1
output_filename=${filename%.mkv}-aac.mkv
audio_stream=$2

if [ -n "$audio_stream" ]
then
    echo "Only converting audio stream #$audio_stream"
    map="-map 0:v -map 0:s -map 0:a:$audio_stream"
else
    map="-map 0"
fi

codecs="-c:v copy -c:s srt -c:a aac"
bitrates="-b:a 320k"

ffmpeg_command="ffmpeg -i $filename $codecs $bitrates $map $output_filename"
echo ""
echo $ffmpeg_command
echo ""

nice -20 $ffmpeg_command && \
(
    chgrp --reference $filename $output_filename
    echo ""
    echo "Created ${output_filename}."
)
