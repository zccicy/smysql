# Introduction

Usually you connect mysql like this:

    mysql -h127.0.0.1 -P3306 -uroot -proot mydbx

Howerver, it's too long.
This project aims to make it possible to connect mysql like ssh.
Write a config file like .ssh/config and type:

    smysql mydb

# Usage

    smysql mydb
    # in put mysqlpasswd OR yourpasswd if necessary

"mydb" is just a example, you can configure it as you like

# Install

    git clone "https://git.oschina.net/mrytsr/smysql.git" ~/smysql
    chmod +x ~/smysql/smysql
    export PATH=$PATH:~/smysql

    mkdir ~/.smysql
    echo "
    host mydb
        user root
        passwd root
        port 3306
        hostname localhost
        database test
    " > .smysql/config

Then connect your db with:

    smysql mydb


# Config

Edit ~/.smysql/config

    host mydb              # db alias, required
        user root          # required
        passwd root        # if not set, use '' by default
        port 3306          # if not set, use 3306 by default
        hostname localhost # if not set, use localhost by default
        database test      # if not set, use test by default

    host mydb2
        user root
        passwd aes256:U2FsdGVkX1+Q5kHQ75TEBbYHerWPCx3iCBiUE1f
        hostname localhost
        database test

    ...

As to the passwd line, you can encrypt it with aes256
smysql-passwd can gen this encryped-passwd for you
Run:

    smysql-passwd

then input mysql-passwd, enter key
input your-passwd twice, enter key
then copy the key generated
which is started with aes256, the smysql program will reconize this head
this is a example of the generated key

    aes256:U2FsdGVkX19mp18FWCG/IY9hWxdauO/CZdcOF+BGFHA=
