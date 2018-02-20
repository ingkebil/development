# Mysql

   1. [Connect](#1-connect)

## 1. Connect
To connect to the mysql databases at clinical genomics we need an active ssh connection to rastapopolous. Add this to a script for instance named: "mysql-db_rasta.sh"
```Bash
# Kill all previous connections
pkill -f “ssh -fN”

# Create an ssh connection
ssh -fN -L 3308:localhost:3308 [your_user_name]@rastapopoulos.scilifelab.se
```

Start the connection using:
```Bash
sh ./mysql-db_rasta.sh
```

Connect through an mysql database manager like [Sequel pro](https://www.sequelpro.com/).
Information on database user name port etc is found in the Clinical Genomics github [server repo](https://github.com/Clinical-Genomics/servers).
