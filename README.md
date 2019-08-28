# packer-flexbuilds
A collection of Hashicorp Packer images for various Cloud Platforms (mostly related automation, containers, and Kubernetes)

## General

I created this repository, because every other packer repo that I found contained very specific packer builds. Even some of the more flexible packer builds were specific in what applications are installed at the time of build. I didn't want this limitation. Additionally, I wanted this project to be driven by variables, so that Jenkins or any other human/platform could provide their own methods for simply deploy any combinations of applications into their packer builds. For additional details on project goals, read through the TODO section. As the project matures, I'm sure it will go through quite a lot of changes, and as it does, I'll start to add more formalized structure around how/what gets added to the `install` directory in each of the packer build folders.

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
- Add summary for `INSTALLED` or `FAILED` at the end of the packer build
- Pull `.packer`, `packer-build`, and `packer-clean` into root folder (needs to be flexible)
- Create Jenkinsfile and start CI testing (jenkins.jinkit.com), along with report-back webhooks
- Add additional OS/Distro exampls (or turn into flexible model)
- Allow for the creation of users
- Implement leave privilege model
- Add additional application examples
- Add user-driven application model
- Allow Docker to pull images in advance
- Add additional security models
