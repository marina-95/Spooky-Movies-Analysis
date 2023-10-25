# 🎃 Spooky Movies - Análisis
![logo-2](https://github.com/marina-95/Spooky-Movies-Analysis/assets/144913530/f9d232e6-af95-477e-8846-748cfca3b1cb)

## Tabla de Contenido

## Introducción

## Herramientas utilizadas
- SQL Server
- Power BI
- Canva

## Diagrama entidad relación
![diagrama E-R-2](https://github.com/marina-95/Spooky-Movies-Analysis/assets/144913530/eb8122ae-9f07-40f3-88d2-13c9db3bd017)

## Preguntas y respuestas
**1)¿Cuáles son las películas más populares?**

````sql
select
        top 5 original_title as Titulo_Pelicula
from [dbo].[horror_movies]
order by popularity desc;
````
#### Respuesta:
| Titulo_Pelicula    |
| ------------------ |
| Orphan: First Kill |
| Beast              |
| Smile              |
| The Black Phone    |
| Presencias         |

***

**2) ¿Cuáles son las películas que han recaudado más dinero en la taquilla?**

````sql
select
        top 5 original_title as Titulo_Pelicula,
		    revenue as Ganancia
from [dbo].[horror_movies]
order by revenue desc;
````
#### Respuesta:
| Titulo_Pelicula    | Ganancia    |
| ------------------ |-------------|
| It                 | 701.842.551 |
| World War Z        | 531.865.000 |
| The Meg            | 530.243.742 |
| It Chapter Two     | 473122525   |
| Jaws               | 470653000   |

***

**3) ¿Cuáles son las películas más largas en términos de minutos de duración?**

````sql
select	
		top 5 original_title as Titulo_Pelicula,
		runtime as Duracion
from [dbo].[horror_movies]
order by runtime desc;
````
#### Respuesta:
| Titulo_Pelicula    | Duracion |
| ------------------ |----------|
| Machine Learning   | 683      |
| Broken Saints      | 626      |
| Kingdom Hospital   | 608      |
| DAU. Degeneration  | 369      |
| Jigoku shojo       | 360      |

***

**4) ¿Qué sagas cinematográficas cuentan con el mayor número de películas producidas?**

````sql
select	
		top 5 collection_name as Nombre_Coleccion, 
		count(*) as Cantidad_Peliculas
from [dbo].[horror_movies]	
where collection_name != 'NA'
group by collection_name
order by Cantidad_Peliculas desc;
````
#### Respuesta:
| Nombre_Coleccion              | Cantidad_Peliculas |
| ----------------------------- |--------------------|
| Honto Ni Atta! Noroi no Video | 63                 |
| Maneater Series               | 26                 |
| Fuuin Eizou                   | 20                 |
| Troublesome Night Collection  | 20                 |
| The Amityville Collectio      | 17                 |

***

**5) ¿Cuáles son las películas más populares estrenadas en Halloween?**

````sql
select	
		top 5 original_title as Titulo_Pelicula, 
		release_date as Fecha_Estreno 
from [dbo].[horror_movies]
where datepart(day, release_date) = 31 and datepart(month, release_date) = 10
order by popularity desc;
````
#### Respuesta:
| Titulo_Peliculas          | Fecha_Estreno |
| ------------------------- |---------------|
| REC 4: Apocalipsis        | 2014-10-31    |
| 28 Days Later             | 2002-10-31    |
| Army of Darkness          | 1992-10-31    |
| La Leyenda de la Nahuala  | 2007-10-31    |
| Zombie Wars               | 2007-10-31    |

***

**6) ¿En qué década se estrenaron más películas?**

````sql
select	
		(floor(year(release_date) / 10) * 10) as Decada, 
		count(*) as Cantidad_Peliculas
from [dbo].[horror_movies]
group by (floor(year(release_date) / 10) * 10)
order by Cantidad_Peliculas desc;
````
#### Respuesta:
| Decada   | Cantidad_Peliculas |
| -------- |--------------------|
| 2010     | 13.388             |
| 2000     | 5.670              |
| 2020     | 5.626              |
| 1980     | 2.563              |
| 1990     | 2.558              |
| 1970     | 1.626              |
| 1960     | 769                |
| 1950     | 340                |
