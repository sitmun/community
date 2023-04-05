[OAD(docs/swagger.yaml)]

## Autenticación

### Accede con correo electrónico / contraseña
!!! info "POST /api/authenticate"
Se solicita un JSON Web Token de acceso para que un usuario pueda operar con el resto de API.
La solicitud incluye el identificador de usuario y la contraseña.

Una solicitud correcta se indica mediante un código de estado HTTP `200 OK`.

#### Parámetros

##### Cabecera

**`accept`** string

| Nombre         | Tipo   | Obligatorio        | Valor               |
|----------------|--------|--------------------|---------------------|
| `accept`       | string |                    | `application/json`  |
| `content-type` | string | :heavy_check_mark: | `application/json`  |

##### Parámetros cuerpo

---


**Endpoint:** `/api/authenticate`

**Método:** POST

**Content-Type (petición):** application/json

**Contenido (petición):** 

**Estado (respuesta)**

| Código | Descripción                                |
|--------|--------------------------------------------|
| `200`  | Se ha obtenido un JSON Web Token de acceso |
| `401`  | No autorizado                              |

**Content-Type (respuesta 200):** application/json

**Contenido (respuesta 200)**: application/json

| Nombre de la propiedad | Tipo   | Descripción        |
|------------------------|--------|--------------------|
| id_token               | string | JSON Web Token     |

**Cabecera (respuesta)**

| Nombre de la propiedad | Descripción                |
|------------------------|----------------------------|
| Authorization          | `Bearer ` + JSON Web Token |

**Petición de muestra**

```bash
curl https://[SITMUN]/api/authenticate --header 'Content-Type: application/json' --request POST --data-binary @- <<BODY
{
  "username": "[USUARIO]",
  "password": "[CONTRASEÑA]"
}
BODY
```

!!! Nota de uso 

    En el ejemplo anterior, deberías reemplazar **[SITMUN]** por el dominio, puerto y contexto donde está
    desplegado **SITMUN Backend**, **[USUARIO]** por un identificador válido de usuarioy **[CONTRASEÑA]**
    por la contraseña del usuario. 

**Respuesta de muestra**

Si la respuesta tiene un código de estado HTTP `200 OK` tendrá una cabecera `Authorization` 
que comenzará con `Bearer` y separado por un espacio en blanco está un **JSON Web Token**.

```json
{
  "id_token": "[JSON Web Token]"
}
```

!!! Nota de uso 

    En el ejemplo anterior, **[JSON Web Token]** será igual al token de la cabecera **Authorization**.
