https://www.youtube.com/watch?v=UGfteFq_6Co
https://www.tecmint.com/install-postgresql-with-pgadmin4-on-linux-mint/
https://www.postgresql.org/download/linux/ubuntu/



sudo -i -u postgres
psql
\q

alter user postgres with password '3898';

startPg &

cd pgadmin4/
source pgadmin4env/bin/activate
python3 pgadmin4env/lib/python3.10/site-packages/pgadmin4/pgAdmin4.py

