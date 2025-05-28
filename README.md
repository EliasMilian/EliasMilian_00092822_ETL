# 📦 ETL PARCIAL 2 – README

> **Objetivo:**  
> Levantar un contenedor SQL Server 2022, restaurar las bases *AdventureWorks* (OLTP y DW) y ejecutar un paquete SSIS que carga tablas clave del OLTP al DW.  
> Contraseña del usuario **sa** → **Admin2002**

---

## 1 · Requisitos

| Herramienta | Versión mín. | Notas de instalación |
|-------------|-------------|----------------------|
| **Docker Desktop** | 4.x | <https://www.docker.com/> |
| **Visual Studio 2022 Community** | 17.x | Extensión “SQL Server Integration Services Projects” |
| **Azure Data Studio** *(opcional)* | — | Restaurar .bak y lanzar queries |
| Terminal (PowerShell/ bash) | — | Incluido en Win10/11 |

---

## 2 · Clonar el repositorio

bash
git clone https://github.com/TuUsuario/ETL_Parcial2.git
cd ETL_Parcial2


## LEVANTAR EL DOCKER 

docker run -d `
  -e "ACCEPT_EULA=Y" `
  -e "SA_PASSWORD=Admin2002" `
  -p 1433:1433 `
  --name sql_server_2022 `
  mcr.microsoft.com/mssql/server:2022-latest


## RESTAURAR LAS BASES
docker cp backups/. sql_server_2022:/var/opt/mssql/data/

##5 · Ejecutar el paquete SSIS
Abre ETL_Parcial2.sln en Visual Studio.

Confirma las Connection Managers

yaml
Copiar
Editar
Server : localhost,1433
User   : sa
Pass   : Admin2002
DB     : AdventureWorks2022 / AdventureWorksDW2022
