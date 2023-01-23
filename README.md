*Note: I wrote Owl organically for myself and have not yet had the time to
genericize the whole thing, so use at your own risk and look out for hardcoded
filepaths and other such idiosyncrasies.*

# Owl

Owl is a timelapse generator for the Raspberry Pi with an attached camera module. Place it on a Pi and face it towards an area, and timelapse videos will be automatically uploaded to an S3 bucket as time goes on.

## Setup

### Prerequisites

- A Raspberry Pi with the [camera module](https://www.raspberrypi.com/products/camera-module-v2/) installed
- An S3 bucket
- ffmpeg
- Ruby 3+
- [`s3fs`](https://github.com/s3fs-fuse/s3fs-fuse)
  - Mount your S3 bucket to a location like `~/s3`

### Installation

``` sh
crontab -e
```

Insert this line into your crontab file:
```cron
# Replace ~/s3 with the mount point for your S3 bucket
@reboot sleep 10 && s3fs glacials-owl ~/s3 -o allow_other -o umask=0007,uid=1001,gid=1001 && mkdir -p ~/s3/ops ~/s3/timelapse/closet/photos
```

Save and quit, then reboot your machine or run the line from cron manually.
