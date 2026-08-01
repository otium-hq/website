# Website 🌐

![](https://img.shields.io/gitlab/pipeline-status/otium-hq/website?branch=main&logo=gitlab)
![](https://img.shields.io/badge/site-otium.run-9A671D)
![](https://img.shields.io/badge/host-s3%20%2B%20cloudfront-FF9900?logo=amazon-aws)

> otium.run marketing site — single-file static page.

## About

Static site served from S3 behind CloudFront at [otium.run](https://otium.run).
Single-file HTML, no build step.

## Infrastructure

| Piece        | Value                                             |
|--------------|---------------------------------------------------|
| S3 bucket    | `otium-run` (us-east-1, private, OAC-only)         |
| CloudFront   | `E2UM72YJIUOGWD` — aliases `otium.run`, `www.otium.run` |
| TLS cert     | ACM (us-east-1), DNS-validated                     |
| DNS          | Namecheap — apex `ALIAS` + `www CNAME` → CloudFront |

## Deploy

Push to `main`. The `.gitlab-ci.yml` pipeline runs `aws s3 sync` to the bucket
and invalidates the CloudFront distribution. AWS creds come from masked CI/CD
variables `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`.
