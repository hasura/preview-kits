## Getting started

1. Install the dev build of the CLI for your machine from `../cli`

```
mv ../cli/cli-hasura-darwin-amd64 /usr/local/bin/hasura-dev
chmod +x /usr/local/bin/hasura-dev
```

2. Run hasura + postgres

**For linux**
If you're on linux first enable `network_mode: host`.
Edit docker-compose.yaml and uncomment the line and then bring everything up!
```
vim docker-compose.yaml
docker-compose up -d
```

**For mac/windows**
```
docker-compose up -d
```

3. Run the graphql-service that we will do a remote join with

```
cd functions/createUser
npm i
npm start
```

4. Run the migrations to create the table

```
hasura-dev migrate apply
```

5. (For linux only) Change the service endpoint in the metadata file
```
cd migrations/metadata.yaml
#Edit the file with your favorite editor and comment out the right things
vim up.yaml
```

6. Apply metadata to create the action etc
```
hasura-dev metadata apply
```

7. Run the service
```
cd functions/createUser
npm start
```

8. *Synchronous*: Open the hasura console and try the mutation!
```
hasura-dev console
```

8. *Asynchronous*: To try the async mutation try the following

```
#Change "kind: synchronous" in metadata.yaml
vim migrations/metadata.yaml

#Apply the new metadata
hasura-dev metadata apply

#Add a delay to the action function to make it deliberately slow
vim functions/createUser/index.js

#Restart the function
cd functions/createUser
npm start

#Restart the function
cd functions/createUser
npm start

#Try out the mutation!
hasura-dev console
```
