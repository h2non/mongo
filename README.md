# h2non/mongo-volumeless

This is the Git fork repo for the Docker **unofficial** volumeless images (see [official images here](https://docs.docker.com/docker-hub/official_repos/)) for [mongo](https://registry.hub.docker.com/_/mongo/). See [the Docker Hub page](https://registry.hub.docker.com/_/mongo/) for the full readme on how to use this Docker image and for information regarding contributing and issues.

**NOTE**: this repo has the same Dockefiles manifests as the official Mongo images but just it simply ignores the `VOLUME` directive, tuning them into `volumeless` and therefore, stateless containers.

## Why volumeless?

Simple: sometimes you need a more predictable, deterministic, stateless, immutable, truly ephemeral container.

In scenarios like automated testing, integration testing, QA or local development it can be very handy.

## Oh, really? Can you show me an example?

Sure.

Let's say you want have an app that's consuming Mongo and you want to provide it along with an immutable constainer that has preloaded data that you seed before.

Users running your container will always have deterministic data in the database and data mutations will only persist within the container execution time frame.

Killing the container and runnig it again will restore the database to the initial, predefined state.

This is very useful in development or testing, where you want to provide a concrete database state with seed data.

## Usage

Pull the image, my friend:
```bash
docker pull h2non/mongo-volumeless:3.7
```

Run it, ftw:
```bash
docker run -t h2non/mongo-volumeless:3.4
```

Without killing the container, run whatever you need in order to seed data within the container. Example: 
```bash
./seed-mongo-data.sh
```

Finally, commit the changes creating a forked images in order to preverve the database state:
```bash
docker commit <containerId> my.registry.com/image-name:latest
```

Optionally, you can push it into your registry to make it available for other people:
```bash
docker push my.registry.com/image-name:latest 
```

Congratulations, now you have a new container image that has a predefined state and will always have it everytime the container is destroyed and created again.

## Available tags

- `3.0`
- `3.2`
- `3.4`
- `3.6` -> `latest`
- `3.7`

## License

Same as official Mongo images.
