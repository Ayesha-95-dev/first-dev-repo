# Containerised Flask App — My First DevOps Project

This is the first project in my journey into cloud and DevOps
engineering. It's a small Flask web app, but the app itself isn't the
point — I built it to learn the workflow that surrounds real
applications: containerising them with Docker, version-controlling them,
and getting them ready to deploy. I wanted something I could take from
"code on my laptop" all the way to "running in the cloud," one step at a
time.

## What it does

It's a simple Python web server that returns a greeting when you visit it
in a browser. Deliberately minimal — I kept the app small so I could
focus my attention on everything that happens *around* the code.

## What's under the hood

- **Python + Flask** for the app itself
- **Docker** to package it so it runs the same anywhere, not just on my
  machine
- **Git & GitHub** for version control

## Running it

    docker build -t first-dev-pro .
    docker run -p 5000:5000 first-dev-pro

Then open `http://localhost:5000`.

## The part I'm actually proud of: what broke, and how I fixed it

Honestly, the most useful part of this project wasn't writing the code —
it was the things that went wrong, because fixing them is where I learned
the most.

- My virtual environment wouldn't build at first. The error pointed me to
  a missing system package, and my first fix attempt failed with a 404
  until I realised my package list was out of date. Refreshing it sorted
  it — a small lesson in reading what the error is actually telling you.

- At one point the app showed "connection refused" in the browser. I
  spent a moment confused before realising the server simply wasn't
  running — I'd stopped it. Obvious in hindsight, but it taught me an
  important habit: "it started" and "it works" are not the same thing,
  and you verify by actually checking.

- The trickiest one: Docker couldn't install Flask during the build. The
  final error blamed Flask, but reading further up, the real cause was a
  DNS failure — the container couldn't translate package-server names
  into addresses. It was a networking quirk in my setup, which I fixed by
  pointing it at a reliable DNS server. That one taught me to look past
  the scary last line and find the actual root cause.

## Where this is going

This is a work in progress. Next, I'm deploying it to AWS so it runs on a
real public URL, then adding infrastructure-as-code, an automated
pipeline, and monitoring — building it up one layer at a time.
