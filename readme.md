# Point.RED | NodeJS Server

## Requirements before installation
1.  You already setup point project (https://github.com/point-red/point) in your machine 
2.  The point project database is already available

## Installation
1.  Install NVM (Node Version Manager)

    using curl to download and install NVM
    ```
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```
    
    this script will add new config for nvm to your profile file
    ```
    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    ```
    
    install node for specific version
    ```
    nvm install 14.19.0
    ```
    
    use the installed node
    ```
    nvm use 14.19.0
    ```

    you can check the node version using this command
    ```
    node -v
    ```

2.  Install yarn

    ```
    npm install -g yarn
    ```

3. Install redis

    updating your local apt package cache:
    ```
    sudo apt update
    ```

    install redis
    ```
    sudo apt install redis-server
    ```

    Inside the file, find the supervised directive. This directive allows you to declare an init system to manage Redis as a service, providing you with more control over its operation. The supervised directive is set to no by default. Since you are running Ubuntu, which uses the systemd init system, change this to systemd:
    ```
    . . .

    # If you run Redis from upstart or systemd, Redis can interact with your
    # supervision tree. Options:
    #   supervised no      - no supervision interaction
    #   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
    #   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
    #   supervised auto    - detect upstart or systemd method based on
    #                        UPSTART_JOB or NOTIFY_SOCKET environment variables
    # Note: these supervision methods only signal "process is ready."
    #       They do not enable continuous liveness pings back to your supervisor.
    supervised systemd

    . . .
    ```

    Then, restart the Redis service to reflect the changes you made to the configuration file:
    ```
    sudo systemctl restart redis.service
    ```

    you can check the redis status by using this command
    ```
    sudo systemctl status redis
    ```

4.  Clone point-node project from github

    using ssh
    ```
    git clone git@github.com:point-red/point-node.git
    ```

5.  Install project dependencies

    go to project directory
    ```
    cd point-node
    ```

    make sure you use installed node version
    ```
    nvm use 14.19.0
    ```

    install the dependecies
    ```
    yarn install
    ```

6.  Create .env file

    create .env file by copy .env.example
    ```
    cp .env.example .env
    ```
    
    complete the .env file variable

7.  Try to run the test

    ```
    yarn run test
    ```
    NB: you can check at the package.json file to see commands that available on this project

8.  If test runs well, now you can run the project on your machine

    ```
    yarn run dev
    ```

9.  Congratulation, now you can work with point-node project 🚀🚀🚀

