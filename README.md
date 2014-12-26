trigrid
=======

This little SQL function build a triangular grid like this kind

![](effe-recherche.jpg)

and result is like this

![](trigrid.png)


-- créer une table tirgrid pour l'Irak
<br>
drop table IF EXISTS iraq_trigrid;<br>
create table iraq_trigrid(gid integer,tx integer, ty integer);<br>
SELECT AddGeometryColumn ('','iraq_trigrid','the_geom',4326,'POLYGON',2);<br>
select trigrid (38.6717,50,50,44,0.13,4326,'iraq_trigrid');<br>
CREATE INDEX sidx_trigrid ON iraq_trigrid USING GIST ( the_geom );<br>
CREATE UNIQUE INDEX idx_trigrid_l1 ON iraq_trigrid (gid);<br>
select count(*) from iraq_trigrid;<br>
 

Produire le grid en degrés.<br>
A Argus : pt_x, pty = coord start grid<br>
gx = largeur grid<br>
gy = hauteur grid<br>
c = longueur des côtés<br>
epsg = code epsg des unités de mesures<br>
tbl = nom de table de sortie<br>
approx 200 m = 0.002 degr<br>
1 km = 0.013 degr<br>
<br>
E Exemple: select trigrid (-150,36,100,44,0.13,4326,'trigrid_l1');
<br>
O Output : A triangle geometry.
Blog post : http://simonmercier.net/blog/?p=1245

