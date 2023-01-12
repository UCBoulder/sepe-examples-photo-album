# Multi-stage build that pulls in python dependencies to generate static
# photo gallery website, then packages the generated content with a simple 
# web server image that will serve it.

## Begin build layer
FROM docker.io/python:3.11.0-slim as builder

WORKDIR /src

# Pull in photos and other sources
COPY . .

# Install python requirements, then build site
RUN pip install -r requirements.txt
RUN sigal build -v . /build


## Begin runtime layer
FROM docker.io/halverneus/static-file-server:v1.8.8

# Copy static site from build layer to runtime
COPY --from=builder /build /web
