# Pull in the layer of the base image: alpine:3.10.3
FROM alpine:3.10.3                             

# Set maintainer label: maintainer=[your-email]
LABEL maintainer='<>'

# Copy file `README.md` to the image folder `/opt/`
COPY README.md /opt/                                 

# Show the content of the `README.md` during the build process 
RUN cat /opt/README.md                    