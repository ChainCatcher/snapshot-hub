# Snapshot hub

This is a hub for Snapshot network that stores the database and forwards new messages to peers. The hub hold a private keys to sign valid messages.

### Install

1. Install Node.js, clone the repository, then say:
```sh
yarn
```
 
2. Copy [`.env.example`](https://github.com/snapshot-labs/snapshot-hub/blob/master/.env.example), rename it to `.env` and set a value for these config vars:

- `DATABASE_URL`: The database connection string. You will need to run your own MySQL database or use a Cloud service like [JawsDB](https://jawsdb.com).
- `RELAYER_PK`: This is the private key of the hub. The hub counter-sign every accepted message with this key.
- `FLEEK_API_KEY`, `FLEEK_API_SECRET` and `FLEEK_BUCKET` are required keys from [Fleek](https://fleek.co) for pinning on IPNS.

3. Create the database schema

Run this query on the MySQL database to create the initial schema with the required tables: 
https://github.com/snapshot-labs/snapshot-hub/blob/master/src/helpers/schema.sql
### Run

- Use this command to run the hub: 
```sh
yarn start
```

- Go on this page: http://localhost:3000/api if everything is fine it should return details of the hub example: 
```json
{
  "name": "snapshot-hub",
  "network": "livenet",
  "version": "0.1.3",
  "tag": "alpha",
  "relayer": "0x8BBE4Ac64246d600BC2889ef5d83809D138F03DF"
}
```

### Usage

Once your hub is running online, the main hub can relay the messages received to your own hub. Please provide the URL of your Snapshot hub to an admin to make sure it's connected to the network.

#### Load a space setting

To load a space settings in the database you can go on this endpoint http://localhost:3000/api/spaces/yam.eth/poke (change yam.eth with the space you want to activate).
