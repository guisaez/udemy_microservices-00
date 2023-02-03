# Creating a Custom Image

# Use an existing docker iamge as a base

FROM alpine 

# Dowload and install a dependency

RUN apk add --update redis
RUN apk add --update gcc

# Tell the image waht to do when it starts 
# as a container

CMD ["redis-server"]