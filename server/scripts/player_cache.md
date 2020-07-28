# Player Cache System

The player cache keeps an in-memory copy of misc player data when they log in to the server to reduce the need to query the SQL database at runtime (which slightly adds lag). The player cache should be used whenever possible instead of writing queries.

Note: `WEAK` references are not guaranteed to always return the same result. The data returned depends on what is already present in the cache or on the last login time of the character.

## name2account

Returns the account id associated with a char name.

```c
"playerCache"::name2account("Reid")
```

## name2char

Returns the char id associated with a char name.

```c
"playerCache"::name2char("Reid")
```

## name2vault

Returns the Vault account id associated with a char name.

```c
"playerCache"::name2vault("Reid")
```

## char2account

Returns the account id associated with a char id.

```c
"playerCache"::char2account(.@charID)
```

## char2name

Returns the char name associated with a char id.

```c
"playerCache"::char2name(.@charID)
```

## char2vault

Returns the Vault account id associated with a char id.

```c
"playerCache"::char2vault(.@charID)
```

## account2char `[WEAK]`

Returns the char id associated with an account id.
**This is a weak reference**: an account id does not uniquely identify a character.

```c
"playerCache"::account2char(.@accountID)
```

## account2name `[WEAK]`

Returns the char name associated with an account id.
**This is a weak reference**: an account id does not uniquely identify a character.

```c
"playerCache"::account2name(.@accountID)
```

## account2vault

Returns the Vault account id associated with a game account id.

```c
"playerCache"::account2vault(.@accountID)
```

## vault2account `[WEAK]`

Returns the account id associated with a Vault account id.
**This is a weak reference**: a Vault account does not uniquely identify a game account.

```c
"playerCache"::vault2account(.@vaultID)
```

## vault2char `[WEAK]`

Returns the char id associated with a Vault account id.
**This is a weak reference**: a Vault account does not uniquely identify a game character.

```c
"playerCache"::vault2char(.@vaultID)
```

## vault2name `[WEAK]`

Returns the char name associated with a Vault account id.
**This is a weak reference**: a Vault account does not uniquely identify a game character.

```c
"playerCache"::vault2name(.@vaultID)
```
