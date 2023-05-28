### Database Layout

- `.../`
    - `.backups/...` - requested backups will be placed in this folder by default
    - [`members/...`](#members) - member files
    - [`config.json`](#configjson) - json file containing configuration
    - [`index.json`](#indexjson) - json file with file indexes vs their hashes


### `members/...`

sorry we were gonna write something here but my spoons ran out again

### `index.json`

Whenever Pluralsnug is asked to run a command, it will check the hashes of all files that may be edited during the
procedure. If any of the files have different hashes, then they have been edited since the last time a command was run
successfully, and the user is warned to avoid loosing any local edits.

In this event, Pluralsnug will list the affected files, and allow two options:

- Cancelling the command entirely (default)
- Creating a database backup and continuing
- Ignoring and continuing

After a command is completed, Pluralsnug will re-evaluate all affected files and update the index accordingly.

### `config.json`

Planned config tags:

- `HasPasswords` - Optional Boolean, Tracks if the users' api tokens are password encrypted. Defaults to false
- `Services` - List of Objects, Tracks the services that the user syncs between and related information. A list of valid
  services is as follows, with the tags that they allow. All objects have a `Service` tag equal to the name listed.
    - [`PluralKit`](https://pluralkit.me)
        - `System` - String, The system's ID. Can be a friendly 5 letter ID or a UUID
        - `Token` - Optional String, The system's auth token. Ignored if `HasPasswords` is true. If absolutely no token
          is provided, the user will be warned about unexpected behaviour, and execution will continue as normal until a
          crash from unauthenticated actions is met
