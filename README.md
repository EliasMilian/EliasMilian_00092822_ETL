3. Pasos de instalación
3.1 Clonar este repositorio
bash
Copiar
Editar
git clone https://github.com/TuUsuario/ETL_Parcial2.git
cd ETL_Parcial2
3.2 Levantar SQL Server 2022 en Docker
powershell
Copiar
Editar
docker run -d `
  -e "ACCEPT_EULA=Y" `
  -e "SA_PASSWORD=Admin2002" `
  -p 1433:1433 `
  --name sql_server_2022 `
  mcr.microsoft.com/mssql/server:2022-latest
Contraseña del usuario sa: Admin2002
(cámbiala si lo deseas, pero recuerda actualizarla en los pasos siguientes).

3.3 Restaurar las bases de datos
Copia los archivos AdventureWorks2022.bak y AdventureWorksDW2022.bak dentro de la carpeta data del contenedor:

powershell
Copiar
Editar
docker cp backups/. sql_server_2022:/var/opt/mssql/data/
Conéctate al contenedor desde Azure Data Studio o SQLCMD y ejecuta los scripts scripts/restore_oltp.sql y scripts/restore_dw.sql.

4. Ejecutar el ETL
Abre el archivo de solución ETL_Parcial2.sln en Visual Studio.

Si es la primera vez, edita los dos Connection Managers (OLTP y DW) y confirma:

yaml
Copiar
Editar
Server   : localhost,1433
User     : sa
Password : Admin2002
Database : AdventureWorks2022 / AdventureWorksDW2022
Pulsa ▶ Start (o F5).