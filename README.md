# apollo-react-client-state

# Apollo Client State with React Starter Project
This project is for used with the Mastering Apollo Series on WintellectNOW http://www.wintellectnow.com

### Project Setup
Requirements
Node.js (version 8 or later)
Web Browser
Instructions

`Step 1. Clone/Download this repository. If downloading the zip file, then extract the zip file.`

`Step 2. Open a terminal window and change to the folder containing the "package.json" file.`

`Step 3. Run the following commands:`

`$. npm install`

`$. npm run start-rest-server`

`$. Step 4. Open a second terminal window and change to the folder containing the "package.json" file.`

`$. Step 5. Run the following command:`

`$. npm run start-graphql-server`

Step 6. Open a third terminal window and change to the folder containing the "package.json" file.

Step 7. Run the following command:

`$. npm run start-client`

Step 8. Your system's default web browser should open and browse to the URL http://localhost:3000.

Modifying the Project
The server files can be modified in the "server-src" folder. The "server-dist" folder is generated by the "start-server" command. Do not edit the files in the "server-dist" folder as they will be overwritten. The client files can be modified in the "public" and "src" folders. The "src" folder contains the JavaScript code for the Apollo Client and React Components.

FAQ
Question 1. If you have another version of Node.js installed on your system which does not work with this course, then please consider installing NVM (for Mac & Linux) or NVM-Windows to enable the installation of multiple versions of Node.js. Both tools support the installation, management and switching between multiple versions of Node.js. Using these tools, installing Node.js version 8 or later without losing your older version should be possible. This course does not provide support for these tools, the course only suggests using them if needed.

Question 2. The default ports number for the three server applications are as follows:

Web Server: 3000
GraphQL Server: 3010
REST Server: 3020
If your system is running programs on these ports there will be a conflict when these three servers are started. Either disable the other applications running on those ports or change the port numbers for this project's servers within your "package.json" file. To change the port numbers, modify the port values specified in the "config" section of the "package.json". No changes to the JavaScript code is needed as the code reads the environment variables set by the config section.

Question 3. If you are running on Windows and running the above "npm" commands with Cygwin Bash then substitute the above commands with these:

npm run start-rest-server-cygwin

npm run start-graphql-server-cygwin

npm run start-client-cygwin
If you are using the Windows Command Prompt (default on Windows), then use the original commands listed in the instructions.


## Instructions

**The REST service data is provided by the `db.json` file**
**The REST service retrieves data from and saves data to `db.json`, also it watches the file for external changes**
**The Apollo Graphql server uses babel to transpile the source Javascript code**
**The source code is located in the `graphql-server` folder**
**Each time a change made to the source code, Babel re-traspiles the code and the server restarts**
**The React Application server watches changes to its files and restarts automatically**
**The React Application files are located in the `public` and `src` folder**
**Almost all React Applications changes will be made in the `src` folder**


## Creating a development environment

1. Install `Node.js`

2. Clone this repository: `https://github.com/t4d-wintellectnow/apollo-react-client-state-starter-project`

3. `$. npm install`

4. `$. npm run start-rest-server`

5. `$. npm run start-graphql-server`

6. `$. npm run start-client`


## Using Client State

**Configuring Client State**

1. Client State is configured by adding a client state link to the Apollo client link configuration

2. The client state link needs a cache where the client state will be stored, this can be the same cache as used for the GraphQl server queries.

3. a default client state tree can be configured using the defaults option

4. the resolvers must be set to an empty object even if no resolvers are explicitly defined.

```js
import { withClientState } from 'apollo-link-state'

const clientStateLink = withClientState({
  cache,
  defaults: {
    toolName: 'widget tool'
  },
  resolvers: {},
})

const link = split(
  webSocketLink,
  ApolloLink.from([clientStateLink, httpLink])
);
```

**Client Directive**

1. To access a client state via a query the @client directive is used

2. The directive is handled by the client state link to retrieve the data from the client state in the cache

3. Server and client queries can be combined into one query

4. If a server client combined query is "refetched" from the server meaning the cahce is bypassed (a "network only" fetch policy) The local state will be reverted to the value of the defaults option in the client state configuration.

GrapgQl Client Directive:

```js
export const APP_QUERY = qql`
  query App {
    toolName @client,
    widgets: {
      id
      name
      description
      color
      size
      price
      quantity
    }
  }
`
```

## Configuring and Querying Client State

