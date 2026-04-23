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

## Intended Use

- This bucket will be used to store generated video outputs for the project.
