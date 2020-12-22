# Don-Express-Database-Monitor

This is Don Express' database monitor, a simple dockerized pg-admin that is served behind nginx (which may be in the same machine or a different one, or even a docker container). To start, both the email and password environment variables must be defined inside the machine. Please refer to `docker-compose.yml`. The volume allows the connection configuration to be persisted across restarts.

## How to run

To run the project simply type in your terminal: `docker-compose build && docker-compose up -d`.

## Creating a connection to the postgres instance

For security reasons any connection from the browser to the DB instance goes through a SSH tunnel. The following pictures will aid you in creating a connection for sensitive environments.

1. Name the connection
   ![connection name](https://i.ibb.co/h2PTSsR/image.png)

2. Configure the connection from the database's point of view. The user (and password) is the one that will connect to the database i.e. the one that is defined inside the postgres instance. For the majority of use cases the database will be reachable at `127.0.0.1` or `localhost`
   ![db user config](https://i.ibb.co/znyFdHx/image.png)

3. Add SSH tunnel protection. The username in this case is the one that connects to the machine through SSH `(ssh user@host)`, and the smae can be said about the IP. Do not get it mixed up with the previous one. Make sure that you add the _private portion_ (that most likely lives inside the `$HOME/.ssh`) of the identity file.
   ![ssh tunnel config](https://i.ibb.co/kB0z0Zc/image.png)

4. Hit save. If it gives you some kind of error, particularly the one that says that cannot find the public key, try closing and reopening the widget. It's a bit buggy.

### Additional considerations

Needless to say the machine you're connecting through SSH must be listening for ssh connections (usually on port 22). Moreover, the public portion of the rsa key you used on step 3 before must also be present in `$HOME/.ssh/authorized_keys` inside the server.
