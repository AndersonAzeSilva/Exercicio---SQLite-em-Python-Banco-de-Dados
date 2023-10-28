#!pip install pysqlite
import sqlite3

connection = sqlite3.connect ("mydatabasejoseanderson.db")
tabela = connection.cursor();

tabela.execute("CREATE TABLE CADASTRO (NOME, RG, CPF, DATA_NASC)")

connection.commit()

tabela.execute("INSERT INTO CADASTRO VALUES ('Anderson', '355308305', '10916907406', '11/06/1995')") 

connection.commit() 

sql_del = """ DELETE FROM CADASTRO WHERE NOME = 'Anderson' """
tabela.execute(sql_del)
connection.commit()

sql_upd = """UPDATE CADASTRO SET NOME = 'Anderson'
             WHERE NOME = 'Andre' 
           """
tabela.execute(sql_upd)
connection.commit()

print("nLista de todos os registro na tabela:\n")
for i in tabela.execute("SELECT rowid, *FROM CADASTRO ORDER BY NOME"):
    print(i)

sel_search = "SELECT * FROM dados WHERE RG = ?"
tabela.execute(sql_search, [("355308305")])
print (tabela.fetchall())
