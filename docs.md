### Database Layout

- `.../`
    - `.backups/...` - requested backups will be placed in this folder by default
    - [`config.json`](#configjson) - json file containing configuration
    - [`index.json`](#indexjson) - json file with file indexes vs their hashes

### `index.json`

Whenever Pluralsnug is asked to run a command, it will check the hashes of all files that may be edited during the
procedure. If any of the files have different hashes, then they have been edited since the last time a command was run
successfully, and the user is warned to avoid loosing any local edits.

In this event, Pluralsnug will list the affected files, and allow two options:

- Cancelling the command entirely (default)
- Creating a database backup and continuing
- Ignoring and continuing

### `config.json`

Planned config tags:

- `HasPasswords` - Optional Boolean, Tracks if the users' api tokens are password encrypted. Defaults to false
- `Services` - List of Objects, Tracks the services that the user syncs between and related information. A list of valid
  services is as follows, with the tags that they allow. All objects have a `Service` tag equal to the name listed.
    - [`PluralKit`](https://pluralkit.me)
        - `System` - String, The system's ID. Can be friendly 5 letter IDs or UUIDs
        - `Token` - Optional String, The system's auth token. Ignored if `HasPasswords` is true. If absolutely no token
          is provided, the user will be warned about unexpected behaviour, and execution will continue as normal until a
          crash from unauthenticated actions is met
