# Initial Setup and Running App on Local Machine

## Work Environment

There are two environments you will be working in for the exercises today.

1. **Your Computer:** The apps and containers must be run on a Linux machine. A CentOS linux machine has been created for you in your Azure subscription.

2. **Azure Cloud Shell:** The Azure Cloud Shell will be accessed by logging into the Azure Portal (http://portal.azure.com).

Labs 1 and 2 require your local computer. The subsequent labs all use the Azure Cloud Shell.

## Clone Lab Github Repo

On your local computer, you will need to clone the workshop repo to the machine.

1. Start with a terminal on your local computer
2. Clone the Github repo via the command line

    ```
    git clone https://github.com/Azure/blackbelt-aks-hackfest.git   // TODO: Change this URL
    ```

## Get Applications up and running

### Database layer - MongoDB

The underlying data store for the app is [MongoDB](https://www.mongodb.com/ "MongoDB Homepage"). With MongoDB running, we need to import the data for our application.

> **Note:** [Download and install MongoDB](https://www.mongodb.com/download-center#community) if required.

1. Import the data using a terminal session on the jumpbox

    ```bash
    cd ~/blackbelt-aks-hackfest/app/db

    mongoimport --host localhost:27019 --db webratings --collection heroes --file ./heroes.json --jsonArray && mongoimport --host localhost:27019 --db webratings --collection ratings --file ./ratings.json --jsonArray && mongoimport --host localhost:27019 --db webratings --collection sites --file ./sites.json --jsonArray
    ```

### API Application layer - Node.js

The API for the app is written in javascript, running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") and [Express](http://expressjs.com/ "Express Homepage")

1. Update dependencies and run app via node from a shell session on your computer.

    ```bash
    cd ~/blackbelt-aks-hackfest/app/api

    npm install && npm run localmachine
    ```

2. Open a new terminal session on the jumpbox and test the API

    ```bash
    curl http://localhost:3000/api/heroes
    ```
    You can also open up a browser from your desktop and browse to <http://localhost:3000/api/heroes>.  
    
    Using [Postman](https://www.getpostman.com/) is also an option.

### Web Application layer - Vue.js, Node.js

The web frontend for the app is written in [Vue.js](https://vuejs.org/Vue "Vue.js Homepage"), running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") with [Webpack](https://webpack.js.org/ "Webpack Homepage")

1. Open a new shell session on your local computer
2. Update dependencies and run app via node

    ```bash
    cd ~/blackbelt-aks-hackfest/app/web

    npm install && npm run localmachine
    ```
3. Test the web front-end

    The jumpbox has an external DNS name and port 8080 is open. You can browse your running app with a link such as: http://jump-vm-csc4f653357f-q72zm5c4ggcza.eastus.cloudapp.azure.com:8080 

    You can also test from a new terminal session in the jumpbox
    ```bash
    curl http://localhost:8080
    ```

## Clean-up

Close the web and api apps in the terminal windows by hitting `ctrl-c` in each of the corresponding terminal windows
