## How we use ffmpeg to lightweight edit webm files
### In this case, trimming the first 5 seconds and continuing for about 18 seconds total
`$ ffmpeg -ss 5 -i original.webm -to 18 edited.webm`
