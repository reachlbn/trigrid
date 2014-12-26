trigrid
=======

This little SQL function build a triangular grid like this kind

![](effe-recherche.jpg)

and result is like this

![](trigrid.png)


-- créer une table tirgrid level 1
<br>
drop table trigrid_l1;
create table trigrid_l1(gid integer,tx integer, ty integer);
SELECT AddGeometryColumn ('','trigrid_l1','the_geom',4326,'POLYGON',2);
select trigrid (-150,36,100,44,0.13,4326,'trigrid_l1');
CREATE INDEX sidx_trigrid_l1 ON trigrid_l1 USING GIST ( the_geom );
CREATE UNIQUE INDEX idx_trigrid_l1 ON trigrid_l1 (gid);
select count(*) from trigrid_l1;
-- 605200
 
-- créer une table tirgrid level 2
drop table trigrid_l2;
create table trigrid_l2(gid integer,tx integer, ty integer);
SELECT AddGeometryColumn ('','trigrid_l2','the_geom',4326,'POLYGON',2);
select trigrid (-150,36,100,44,0.065,4326,'trigrid_l2');
CREATE INDEX sidx_trigrid_l2 ON trigrid_l2 USING GIST ( the_geom );
CREATE UNIQUE INDEX idx_trigrid_l2 ON trigrid_l2 (gid);
select count(*) from trigrid_l2;
-- 2410968
