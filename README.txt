-- Generado por Oracle SQL Developer Data Modeler 20.2.0.167.1538
--   en:        2020-07-09 22:56:37 CLT
--   sitio:      Oracle Database 11g
--   tipo:      Oracle Database 11g



-- predefined type, no DDL - MDSYS.SDO_GEOMETRY

-- predefined type, no DDL - XMLTYPE

CREATE TABLE calificacion (
    id_pelicula           VARCHAR2(10) NOT NULL,
    calificacion          VARCHAR2(50),
    pelicula_id_pelicula  VARCHAR2(10) NOT NULL
);

CREATE UNIQUE INDEX calificacion__idx ON
    calificacion (
        pelicula_id_pelicula
    ASC );

ALTER TABLE calificacion ADD CONSTRAINT calificacion_pk PRIMARY KEY ( id_pelicula );

CREATE TABLE cine (
    id_cine    VARCHAR2(10) NOT NULL,
    nom_cine   VARCHAR2(100),
    direccion  VARCHAR2(255),
    telefono   VARCHAR2(20)
);

ALTER TABLE cine ADD CONSTRAINT cine_pk PRIMARY KEY ( id_cine );

CREATE TABLE det_sala (
    id_sala               VARCHAR2(10) NOT NULL,
    id_cine               VARCHAR2(10) NOT NULL,
    nombre                VARCHAR2(30),
    num_sala              VARCHAR2(10),
    cant_but              VARCHAR2(10),
    pelicula_id_pelicula  VARCHAR2(10) NOT NULL,
    cine_id_cine          VARCHAR2(10) NOT NULL
);

ALTER TABLE det_sala ADD CONSTRAINT det_sala_pk PRIMARY KEY ( id_sala,
                                                              id_cine );

CREATE TABLE funcion (
    id_sala               VARCHAR2(10) NOT NULL,
    fecha_func            DATE,
    hora_func             DATE,
    id_pelicula           VARCHAR2(10) NOT NULL,
    id_funcion            VARCHAR2(10) NOT NULL,
    pelicula_id_pelicula  VARCHAR2(10) NOT NULL,
    det_sala_id_sala      VARCHAR2(10) NOT NULL,
    det_sala_id_cine      VARCHAR2(10) NOT NULL
);

ALTER TABLE funcion ADD CONSTRAINT funcion_pk PRIMARY KEY ( id_pelicula,
                                                            id_funcion );

CREATE TABLE pelicula (
    id_pelicula  VARCHAR2(10) NOT NULL,
    tit_dist     VARCHAR2(50),
    tit_orig     VARCHAR2(50),
    pais_origen  VARCHAR2(30),
    ano_prod     NUMBER(4),
    web          VARCHAR2(50),
    duracion     VARCHAR2(8),
    fecha_est    DATE,
    resumen      VARCHAR2(500)
);

ALTER TABLE pelicula ADD CONSTRAINT pelicula_pk PRIMARY KEY ( id_pelicula );

CREATE TABLE promocion (
    id_funcion           VARCHAR2(10) NOT NULL,
    descripcion          VARCHAR2(100),
    descuento            VARCHAR2(50),
    funcion_id_pelicula  VARCHAR2(10) NOT NULL,
    funcion_id_funcion   VARCHAR2(10) NOT NULL
);

CREATE UNIQUE INDEX promocion__idx ON
    promocion (
        funcion_id_pelicula
    ASC,
        funcion_id_funcion
    ASC );

ALTER TABLE promocion ADD CONSTRAINT promocion_pk PRIMARY KEY ( id_funcion );

CREATE TABLE rep_info (
    nombre        VARCHAR2(40) NOT NULL,
    nacionalidad  VARCHAR2(50)
);

ALTER TABLE rep_info ADD CONSTRAINT rep_info_pk PRIMARY KEY ( nombre );

CREATE TABLE rep_pelic (
    id_pelicula           VARCHAR2(10) NOT NULL,
    nombre                VARCHAR2(40),
    rol                   VARCHAR2(50),
    pelicula_id_pelicula  VARCHAR2(10) NOT NULL,
    rep_info_nombre       VARCHAR2(40) NOT NULL
);

CREATE UNIQUE INDEX rep_pelic__idx ON
    rep_pelic (
        pelicula_id_pelicula
    ASC );

CREATE UNIQUE INDEX rep_pelic__idxv1 ON
    rep_pelic (
        rep_info_nombre
    ASC );

ALTER TABLE rep_pelic ADD CONSTRAINT rep_pelic_pk PRIMARY KEY ( id_pelicula );

CREATE TABLE subtitulos (
    id_pelicula           VARCHAR2(10) NOT NULL,
    subtitulos            VARCHAR2(30),
    pelicula_id_pelicula  VARCHAR2(10) NOT NULL
);

ALTER TABLE subtitulos ADD CONSTRAINT subtitulos_pk PRIMARY KEY ( id_pelicula );

ALTER TABLE calificacion
    ADD CONSTRAINT calificacion_pelicula_fk FOREIGN KEY ( pelicula_id_pelicula )
        REFERENCES pelicula ( id_pelicula );

ALTER TABLE det_sala
    ADD CONSTRAINT det_sala_cine_fk FOREIGN KEY ( cine_id_cine )
        REFERENCES cine ( id_cine );

ALTER TABLE det_sala
    ADD CONSTRAINT det_sala_pelicula_fk FOREIGN KEY ( pelicula_id_pelicula )
        REFERENCES pelicula ( id_pelicula );

ALTER TABLE funcion
    ADD CONSTRAINT funcion_det_sala_fk FOREIGN KEY ( det_sala_id_sala,
                                                     det_sala_id_cine )
        REFERENCES det_sala ( id_sala,
                              id_cine );

ALTER TABLE funcion
    ADD CONSTRAINT funcion_pelicula_fk FOREIGN KEY ( pelicula_id_pelicula )
        REFERENCES pelicula ( id_pelicula );

ALTER TABLE promocion
    ADD CONSTRAINT promocion_funcion_fk FOREIGN KEY ( funcion_id_pelicula,
                                                      funcion_id_funcion )
        REFERENCES funcion ( id_pelicula,
                             id_funcion );

ALTER TABLE rep_pelic
    ADD CONSTRAINT rep_pelic_pelicula_fk FOREIGN KEY ( pelicula_id_pelicula )
        REFERENCES pelicula ( id_pelicula );

ALTER TABLE rep_pelic
    ADD CONSTRAINT rep_pelic_rep_info_fk FOREIGN KEY ( rep_info_nombre )
        REFERENCES rep_info ( nombre );

ALTER TABLE subtitulos
    ADD CONSTRAINT subtitulos_pelicula_fk FOREIGN KEY ( pelicula_id_pelicula )
        REFERENCES pelicula ( id_pelicula );



-- Informe de Resumen de Oracle SQL Developer Data Modeler: 
-- 
-- CREATE TABLE                             9
-- CREATE INDEX                             4
-- ALTER TABLE                             18
-- CREATE VIEW                              0
-- ALTER VIEW                               0
-- CREATE PACKAGE                           0
-- CREATE PACKAGE BODY                      0
-- CREATE PROCEDURE                         0
-- CREATE FUNCTION                          0
-- CREATE TRIGGER                           0
-- ALTER TRIGGER                            0
-- CREATE COLLECTION TYPE                   0
-- CREATE STRUCTURED TYPE                   0
-- CREATE STRUCTURED TYPE BODY              0
-- CREATE CLUSTER                           0
-- CREATE CONTEXT                           0
-- CREATE DATABASE                          0
-- CREATE DIMENSION                         0
-- CREATE DIRECTORY                         0
-- CREATE DISK GROUP                        0
-- CREATE ROLE                              0
-- CREATE ROLLBACK SEGMENT                  0
-- CREATE SEQUENCE                          0
-- CREATE MATERIALIZED VIEW                 0
-- CREATE MATERIALIZED VIEW LOG             0
-- CREATE SYNONYM                           0
-- CREATE TABLESPACE                        0
-- CREATE USER                              0
-- 
-- DROP TABLESPACE                          0
-- DROP DATABASE                            0
-- 
-- REDACTION POLICY                         0
-- 
-- ORDS DROP SCHEMA                         0
-- ORDS ENABLE SCHEMA                       0
-- ORDS ENABLE OBJECT                       0
-- 
-- ERRORS                                   0
-- WARNINGS                                 0
