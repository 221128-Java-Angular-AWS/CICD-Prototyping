# CICD-Prototyping
This is a repo for documentation and collaboration in establishing a prototype for future P3 CICD pipelines

Issue resolution-
If application was locally packaged on anything other than an AMD architecture (e.g. Arm64), to run app on EC2 Linux instance, use 'sudo docker run -it --rm --platform linux/arm64 imgName:tag'.
If this throws an error, try ' docker run --privileged --rm tonistiigi/binfmt --install all' before containerizing your img.
