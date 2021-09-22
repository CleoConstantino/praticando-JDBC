## Praticando JDBC

Para demonstrar a utilização de JDBC, criei o projeto exercicioJDBC utilizando MAVEN, este projeto utilizará o banco de dados POSTGRES.

## Tabelas do projeto

**Tabela curso:**

    CREATE TABLE public.curso
    (
        id integer NOT NULL DEFAULT nextval('curso_id_seq'::regclass),
        descricao character varying(60) COLLATE pg_catalog."default" NOT NULL,
        numero_creditos integer NOT NULL,
        coordenador character varying(60) COLLATE pg_catalog."default" NOT NULL,
        CONSTRAINT curso_pkey PRIMARY KEY (id)
    )
    
    TABLESPACE pg_default;
    
    ALTER TABLE public.curso
        OWNER to postgres;

**Tabela disciplina:**

    CREATE TABLE public.disciplina
    (
        id integer NOT NULL DEFAULT nextval('disciplina_id_seq'::regclass),
        descricao character varying(60) COLLATE pg_catalog."default" NOT NULL,
        numero_creditos integer NOT NULL,
        curso_id integer NOT NULL DEFAULT nextval('disciplina_curso_id_seq'::regclass),
        CONSTRAINT disciplina_pkey PRIMARY KEY (id),
        CONSTRAINT disciplina_curso_id_fkey FOREIGN KEY (curso_id)
            REFERENCES public.curso (id) MATCH SIMPLE
            ON UPDATE NO ACTION
            ON DELETE NO ACTION
    )
    
    TABLESPACE pg_default;
    
    ALTER TABLE public.disciplina
        OWNER to postgres;

