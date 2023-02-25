# ABOUND Starter Repo - p5.js

This is a starter repository for an ABOUND algorithm written in
[p5.js](https://p5js.org/). 

> **Warning**  
>
> p5.js is meant to run in the context of a web browser. To make it work in a
> server environment, we use [p5js-node](https://github.com/SamuelScheit/p5js-node),
> an unmaintained fork of p5.js. As such, not all p5.js features may be
> supported and existing code may have to be adapted. Further, because the
> `p5js-node` package is no longer available (if it ever was), we use the
> `@mattheath/p5js-node` NPM package to provide this functionality.

* Unsure on what ABOUND is? Check out https://abound.art
* Looking for another language? Check out our other options for starter repos [here](https://abound.art/artists)
* New to p5.js? Learn the basics [here](https://www.typescriptlang.org/docs/handbook/intro.html).
* New to [NodeJS](https://nodejs.org/en/)? It's mostly just an easy way to run JavaScript outside a web browser.

## What is in this repo

This repo includes all of the scaffolding to build an algorithm for ABOUND. That means:

1. Reading in the JSON configuration for a run
2. Generating art using the [p5.js Mandelbrot Set example](https://p5js.org/examples/simulate-the-mandelbrot-set.html)
  * Most of the other starter repos implement a
  [Lorenz attractor](https://en.wikipedia.org/wiki/Lorenz_system), which is also
  perfectly doable here, see the
  [starter-node repo](https://github.com/Abound-art/starter-node) for an example
  of that. We just chose to use a p5.js example directly to better illustrate
  its usage.
3. Writing the output to a file

In short, this repo does everything except implement your art algorithm.

## Run locally + Testing your code

```bash
export ABOUND_CONFIG_PATH=example_input.json
export ABOUND_OUTPUT_PATH=output.png
npm run generate-image
```

Will generate a piece of art at `output.png` that looks like this:

![An example output of the Mandelbrot Set algorithm](/example_output.png)

To start implementing your algorithm, replace the `Config` interface and `draw`
function in [`src/index.ts`](/src/index.ts) with your own. It's
also worth noting that the example algorithm produces raster images, meaning
they're made of pixels and are output as
[PNG](https://en.wikipedia.org/wiki/PNG) files, but you can also write
algorithms that produce vector images, meaning they're made of geometric shapes
and are output as [SVG](https://en.wikipedia.org/wiki/SVG) files, perhaps using
[p5.js-svg](https://github.com/zenozeng/p5.js-svg)

### As a Docker container

To test the algorithm in a Docker container, run:

```bash
./scripts/build_image.sh
./scripts/run_image.sh <config path> <output path>
```

Where `<config path>` defaults to `example_input.json` and `<output path>`
defaults to `output.png`.

## Packaging for Deployment

Algorithms are uploaded to ABOUND as Docker containers. The example algo can be
built by running:

```bash
./scripts/build_image.sh
```

Which will build the example image and tag it `abound-starter-p5js`.

## Deploying on ABOUND 

Head to https://abound.art/artists for the most recent instructions on how to upload
your algorithm once it is written. Make sure to read through the constraints carefully
to make sure that your algorithm conforms to them prior to submission.

Once you're ready to upload, tag and push the image with:

```bash
docker tag <local tag> <image name given by ABOUND>
docker push <image name given by ABOUND>
```

If you haven't changed the example configuration in this repo, the `<local
tag>` defaults to `abound-starter-p5js`.

The `docker push` command will fail if you aren't already authenticated with
your ABOUND credentials.
