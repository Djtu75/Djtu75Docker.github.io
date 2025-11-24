# Djtu75Docker.github.io
# Dockerization Guide (linux)

## Step 0

Try to dockerize an old nextjs project and run into a billion errors
because they've updated the version so much over the past year. Finally
get it working, only for it not to work in a linux vm when it works fine
in windows. Give up on it and just make your own mini webserver.

------------------------------------------------------------------------

## Step 1

-   Boot up your linux vm (mine is a fedora)

------------------------------------------------------------------------

## Step 2

-   Download docker by running these commands

-   First ensure that you have the config manager:

```sudo dnf install dnf-plugins-core```

-   then run this to get all of the docker components:

```sudo dnf config-manager addrepo --from-repofile="https://download.docker.com/linux/fedora/docker-ce.repo"```

-   and install the rest of the docker packages:

```sudo dnf install docker-ce docker-ce-cli containerd.io```

-   it may ask to import open PGP, say yes

-   then run

```sudo systemctl enable docker```

-   and

```sudo systemctl start docker```

-   then finally add docker-compose:

```sudo dnf install docker-compose-plugin```

------------------------------------------------------------------------

## Step 3

-   then to get a test dockerized application run:

```git clone https://github.com/Djtu75/tempwebserver.git```

This downloads a basic python webserver and dockerfiles to serve html as an example.
The docker container itself is made based on python 3.11-slim:

```# Use the official Python 3 image
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Copy current directory contents into the container
COPY . /app

# Expose port 8000 to the host
EXPOSE 8000

# Run a simple HTTP server
CMD ["python", "-m", "http.server", "8000"]
```

The docker-compose.yaml file then sets up the basic port, volume, and data:

```services:
  web:
    build: .
    ports:
      - "8080:8000"
    volumes:
      - .:/app
```

------------------------------------------------------------------------

## Step 4

-   cd into tempwebserver

-   then run 

```docker compose up --build```

-   you should see the container build

-   finally, open up a web browser and connect to localhost:8080

it should look like this:
<img width="975" height="597" alt="image" src="https://github.com/user-attachments/assets/554a1601-bb89-4ed6-b395-b9d3c7fef2c3" />
