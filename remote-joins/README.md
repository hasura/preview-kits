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
cd graphql-services/weather
npm i
npm start
```

4. (For linux only) Change the service endpoint of the graphql service depending on your platform
   in the migrations directory
```
cd migrations/1573259820770_create_remote_schema_weather
#Edit the file with your favorite editor and comment out the right things
vim up.yaml
```

5. Run the migrations to get the sample table and remote join setup

```
hasura-dev migrate apply
```

5. Open the console
```
hasura console
```

## Troubleshooting

- *Inconsistent metadata*
When you open the console if you see an inconsistent metadata error, you might not have started the graphql-service
