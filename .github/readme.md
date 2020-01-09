## parkside-securities/drone

A fork of [drone/drone](https://github.com/drone/drone).

## Modifications
- Add `-tags nolimit` to `scripts/build.sh` so that [the limitation of 5,000 builds per year](https://discourse.drone.io/t/licensing-and-subscription-faq/3839) is lifted.
- Checks `[skip ci]`, `[ci skip]`, `**no ci**` only in the title, and ignore them in the commit message. 
- Add `Dockerfile` and let Quay build the image instead of `.drone.yml`. We don't need to build for multiple architectures and deployment URL is hard-coded, so decided to provide a separate Dockerfile and manage in Quay. 

## Usage
Specify `quay.io/parkside-securities/drone:tag` in [green-bay/drone-server](https://github.com/parkside-securities/green-bay/blob/59780c2d0b763445ea881ec57ed3736c9cd0aa18/drone-server/drone-server.sh#L18), build an AMI, and deploy an EC2 instance with the AMI.

## Original README
Drone is a Continuous Delivery system built on container technology. Drone uses a simple YAML configuration file, a superset of docker-compose, to define and execute Pipelines inside Docker containers. 

<br/>

<img src="https://github.com/drone/brand/blob/master/screenshots/screenshot_build_success.png" style="max-width:100px;" />

Sample Pipeline Configuration:

```yaml
name: default

kind: pipeline
type: docker

steps:
- name: backend
  image: golang
  commands:
    - go get
    - go build
    - go test

- name: frontend
  image: node:6
  commands:
    - npm install
    - npm test

- name: publish
  image: plugins/docker
  settings:
    repo: octocat/hello-world
    tags: [ 1, 1.1, latest ]
    registry: index.docker.io

- name: notify
  image: plugins/slack
  settings:
    channel: developers
    username: drone
```

Documentation and Other Links:

* Setup Documentation [docs.drone.io/installation](http://docs.drone.io/installation/)
* Usage Documentation [docs.drone.io/getting-started](http://docs.drone.io/getting-started/)
* Plugin Index [plugins.drone.io](http://plugins.drone.io/)
* Getting Help [discourse.drone.io](https://discourse.drone.io)
* Build the Enterprise Edition [BUILDING](https://github.com/drone/drone/blob/master/BUILDING)
* Build the Community Edition [BUILDING_OSS](https://github.com/drone/drone/blob/master/BUILDING_OSS)

_Please note the official Docker images run the Drone Enterprise distribution. If you would like to run the Community Edition you can build from source by following the instructions in [BUILDING_OSS](https://github.com/drone/drone/blob/master/BUILDING_OSS)._
