FROM golang:1.11-alpine

# Set /src as working directory
WORKDIR /src/

# Copy source code to folder /src
COPY main.go go.* /src/

# Build the GO app as myapp binary and move it to /usr/
RUN CGO_ENABLED=0 go build -o /usr/myapp

# Run the service myapp when a container when a container of this image is launched
CMD ["/usr/myapp"]