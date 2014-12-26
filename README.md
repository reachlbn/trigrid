trigrid
=======

This little SQL function build a triangular grid like this kind

![](effe-recherche.jpg)

and result is like this

![](trigrid.png)


-- créer une table tirgrid pour l'Irak
<br>
drop table IF EXISTS iraq_trigrid;
create table iraq_trigrid(gid integer,tx integer, ty integer);
SELECT AddGeometryColumn ('','iraq_trigrid','the_geom',4326,'POLYGON',2);
select trigrid (38.6717,50,50,44,0.13,4326,'iraq_trigrid');
CREATE INDEX sidx_trigrid ON iraq_trigrid USING GIST ( the_geom );
CREATE UNIQUE INDEX idx_trigrid_l1 ON iraq_trigrid (gid);
select count(*) from iraq_trigrid;
 

--/******************************************************************************************
--D Description: Créer un grid de triangle. Ce grid s'inspire de cette image
-- (http://pinterest.com/pin/145170787958002611/). Il est préférable de
-- produire le grid en degrés.
--A Argus : pt_x, pty = coord start grid
-- gx = largeur grid
-- gy = hauteur grid
-- c = longueur des côtés
-- epsg = code epsg des unités de mesures
-- tbl = nom de table de sortie
-- approx 200 m = 0.002 degr
-- 1 km = 0.013 degr
-- 
--E Exemple: select trigrid (-150,36,100,44,0.13,4326,'trigrid_l1');
-- 
--O Output : A triangle geometry.
--Blog post : http://simonmercier.net/blog/?p=1245
--******************************************************************************************/
