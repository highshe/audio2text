# audio2text pipeline
audio2text  ffmpeg wisper gp4correct


#step1 

ffmpeg -i input.mp3 -f segment -segment_times 0,600,1200,1800,2400,3000,3600,4200 -reset_timestamps 1 -map 0:a -c:a copy output_%03d.mp3


#step2

source myopenai
curl  https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F model="whisper-1" \
  -F file="@./output_001.mp3" |tee wisout



