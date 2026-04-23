# Internal Notes

This document records project-operational information that is not intended for
the presentation itself.

## S3 Bucket

- Bucket name: `ita-promptathlon2026`
- Region: `eu-central-1`
- Base URL: `https://ita-promptathlon2026.s3.eu-central-1.amazonaws.com/`

## Access Behavior

- Public `GetObject` access is currently working for at least the checked test
  object.
- Verified object URL:
  `https://ita-promptathlon2026.s3.eu-central-1.amazonaws.com/empty-test-file.txt`
- Verified result on April 23, 2026: `HTTP/1.1 200 OK`

## Video Sharing Update

- The project will not use S3 for sharing generated videos.
- Video sharing will use HeyGen-hosted playback links instead.
- First video link:
  `https://app.heygen.com/videos/5d23531a251c41719184ced6b1c1d097`
