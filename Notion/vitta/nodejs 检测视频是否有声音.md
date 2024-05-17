- 安装 [node-fluent-ffmpeg](https://github.com/fluent-ffmpeg/node-fluent-ffmpeg.git)
- function

```Plain
const domain = require('domain');
const VOLUME_THRESHOLD = -50;
function getMeanVolume (streamUrl, callback) {
        new ffmpeg({ source: streamUrl }).audioFilter('volumedetect')
    .addOption('-f', 'null')
    .addOption('-t', '10')
    .on('start', function (ffmpegCommand) {
        console.log('Output the ffmpeg command', ffmpegCommand);
    })
    .on('end', function (stdout, stderr) {
        console.log('------');
        console.log(stdout);
        console.log(stderr);
        // find the mean_volume in the output
        let meanVolumeRegex = stderr.match(/mean_volume:\s(-?[0–9]\d*(\.\d+)?)/);
        // return the mean volume
        if (meanVolumeRegex) {
            let meanVolume = parseFloat(meanVolumeRegex[1]);
            return callback(meanVolume);
        }

        // if the stream is not available
        if (stderr.match(/Server returned 404 Not Found/)) {
            return callback(false);
        }
        return callback();
    })
    .saveToFile('/dev/null');
}


d.on('error', (e) => {
options.logger.error(e);
});
d.run(await getMeanVolume(video.videoUrl, (meanVolume) => {
if (meanVolume <= VOLUME_THRESHOLD) {
    console.log('sounds too low');
    return video._id;
}
}));
```

-%20%E5%AE%89%E8%A3%85%20%5Bnode-fluent-ffmpeg%5D(https%3A%2F%2Fgithub.com%2Ffluent-ffmpeg%2Fnode-fluent-ffmpeg.git)%0A-%20function%0A%60%60%60%0Aconst%20domain%20%3D%20require('domain')%3B%0Aconst%20VOLUME_THRESHOLD%20%3D%20-50%3B%0Afunction%20getMeanVolume%20(streamUrl%2C%20callback)%20%7B%0A%09%09new%20ffmpeg(%7B%20source%3A%20streamUrl%20%7D).audioFilter('volumedetect')%0A%09.addOption('-f'%2C%20'null')%0A%09.addOption('-t'%2C%20'10')%0A%09.on('start'%2C%20function%20(ffmpegCommand)%20%7B%0A%09%09console.log('Output%20the%20ffmpeg%20command'%2C%20ffmpegCommand)%3B%0A%09%7D)%0A%09.on('end'%2C%20function%20(stdout%2C%20stderr)%20%7B%0A%09%09console.log('------')%3B%0A%09%09console.log(stdout)%3B%0A%09%09console.log(stderr)%3B%0A%09%09%2F%2F%20find%20the%20mean_volume%20in%20the%20output%0A%09%09let%20meanVolumeRegex%20%3D%20stderr.match(%2Fmean_volume%3A%5Cs(-%3F%5B0%E2%80%939%5D%5Cd*(%5C.%5Cd%2B)%3F)%2F)%3B%0A%09%09%2F%2F%20return%20the%20mean%20volume%0A%09%09if%20(meanVolumeRegex)%20%7B%0A%09%09%09let%20meanVolume%20%3D%20parseFloat(meanVolumeRegex%5B1%5D)%3B%0A%09%09%09return%20callback(meanVolume)%3B%0A%09%09%7D%0A%0A%09%09%2F%2F%20if%20the%20stream%20is%20not%20available%0A%09%09if%20(stderr.match(%2FServer%20returned%20404%20Not%20Found%2F))%20%7B%0A%09%09%09return%20callback(false)%3B%0A%09%09%7D%0A%09%09return%20callback()%3B%0A%09%7D)%0A%09.saveToFile('%2Fdev%2Fnull')%3B%0A%7D%0A%0A%0Ad.on('error'%2C%20(e)%20%3D%3E%20%7B%0Aoptions.logger.error(e)%3B%0A%7D)%3B%0Ad.run(await%20getMeanVolume(video.videoUrl%2C%20(meanVolume)%20%3D%3E%20%7B%0Aif%20(meanVolume%20%3C%3D%20VOLUME_THRESHOLD)%20%7B%0A%20%20%20%20console.log('sounds%20too%20low')%3B%0A%20%20%20%20return%20video._id%3B%0A%7D%0A%7D))%3B%0A%60%60%60