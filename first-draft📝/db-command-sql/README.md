-

- SQL db
Alter table very costy

CREATE DATABASE message_boards;

Whereas nosql, you just use and once you save something it is ok

\c message_boards;
-- \connect message_boards works too

-- see all databases
\l

-- see all tables in this database, probably won't see anything
\d

-- see all available commands
\?

-- see available queries
\h

-- run a shell command
\! ls && echo "hi from shell!"
