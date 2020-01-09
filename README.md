## parkside-securities/drone

A fork of [drone/drone](https://github.com/drone/drone).

## Modifications
- Add `-tags nolimit` to `scripts/build.sh` so that [the limitation of 5,000 builds per year](https://discourse.drone.io/t/licensing-and-subscription-faq/3839) is lifted.
- Checks `[skip ci]`, `[ci skip]`, `**no ci**` only in the title, and ignore them in the commit message. 
- Add `Dockerfile` and let Quay build the image instead of `.drone.yml`. We don't need to build for multiple architectures and deployment URL is hard-coded, so decided to provide a separate Dockerfile and manage in Quay. 

## Usage
Specify `quay.io/parkside-securities/drone:tag` in [green-bay/drone-server](https://github.com/parkside-securities/green-bay/blob/59780c2d0b763445ea881ec57ed3736c9cd0aa18/drone-server/drone-server.sh#L18), build an AMI, and deploy an EC2 instance with the AMI.
