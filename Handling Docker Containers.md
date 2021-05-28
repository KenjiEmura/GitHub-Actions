# Handling Docker Containers

Check the docker_container.yaml file to see the implementation.

With the `services` property, we can set a structure similar to a docker-compose file.

Usually, `ENTRYPOINT` uses an array which first argument is a path to the command that we want to execute and then the arguments that the command receives, for example, if we were to run the `echo` command, we would have to enter the path to the file of the executable command which can be obtained by running `type -a echo` and after that the string or the element that we want to print, so it will look like this:
`ENTRYPOINT ['/bin/echo', 'Hello']`
If we add after that a `CMD ['world!!']` that last command will act as a third argument for the `ENTRYPOINT`, so `Hello world!!` will be printed.

We can also run diferent containers along the different steps of our workflow by putting the image in the `uses:` property. We can modify the default `ENRYPOINT` of the image by using the `with` property. Unlike the default `ENTRYPOINT`'s behaviour, in Github Actions, we define the entrypoint with just the path to the executable.