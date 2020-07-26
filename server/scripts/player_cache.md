# Player Cache System

The player cache keeps an in-memory copy of misc player data when they log in to the server to reduce the need to query the SQL database at runtime (which slightly adds lag). The player cache should be used whenever possible instead of writing queries.

## name2account

Returns the account id associated with a char name.

```c
"playerCache"::name2account("Reid");
```

## name2char

Returns the char id associated with a char name.

```c
"playerCache"::name2char("Reid");
```

## char2account

Returns the account id associated with a char id.

```c
"playerCache"::char2account(.@charID);
```

## account2char

Returns the char id associated with an account id.
**This is a weak reference**: an account id does not uniquely identify a character.

```c
"playerCache"::account2char(.@accountID);
```

## vault2account

Returns the account id associated with a Vault account id.
**This is a weak reference**: a Vault account does not uniquely identify a game account.

```c
"playerCache"::vault2account(.@vaultID);
```

## account2vault

Returns the Vault account id associated with a game account id.

```c
"playerCache"::account2vault(.@accountID);
```
