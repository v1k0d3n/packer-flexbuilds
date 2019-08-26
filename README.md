# packer-flexbuilds
A collection of Hashicorp Packer images for various Cloud Platforms (mostly related automation, containers, and Kubernetes)

## General

This repository provides a flexible, variable-driven method to produce packer images. For further details, read through the TODO section.

## Notice

I've decided to change the format for how the packer images in this repo are executed. Instead of having a collection of specific folders per packer artifact (which seemed incredibly wasteful and redundant), I'm forcing `BASH` environment variables to drive each of the installs. This way, the only thing that needs to be added are semi-intelligent scripts tied to a shell variable. When that variable is then called, either manually through a shell session or through a CI/CD system like Jenkins, only the things required are installed. Consideration must be given when ordering the installs, but this will simplify the overall repository greatly.

***NOTE:*** *these changes will occur over the course of the next few days.*

## Locate

If you want to find your image after creation, you can run the following commands:
```

# Source the .packer file:
source .packer

aws ec2 describe-images --region "${aws_region}" \
  --filters Name=tag-key,Values=ami Name=tag-value,Values=${aws_ami_name} \
  --query 'Images[*].{ID:ImageId}'
```

## Contributions

Please consider contributing rather than forking for the purpose of "saving" this repository. All contributions will be considered and reviewed. CI/CD coming soon! I'm just trying to decide if I should use [GitHub Actions](https://github.com/features/actions) or a project-level Jenkinsfile.

## TODO

These are some high-level items that need completed:
- Create Jenkinsfile and start CI testing (jenkins.jinkit.com), along with report-back webhooks
- Add additional OS/Distro exampls (or turn into flexible model)
- Allow for the creation of users
- Implement leave privilege model
- Add additional application examples
- Add user-driven application model
- Allow Docker to pull images in advance
- Add additional security models
