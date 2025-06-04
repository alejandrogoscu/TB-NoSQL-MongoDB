
# Proyecto MongoDB - Red Social

Este proyecto consiste en desarrollar una base de datos de red social utilizando MongoDB desde la terminal. Se deben crear las colecciones `users` y `posts`, e insertar, actualizar, consultar y eliminar datos según las instrucciones descritas a continuación.

---

## 1. Desarrollar el Proyecto

### Estructura de la Base de Datos

Se deben crear las siguientes **colecciones**:

- `users`
- `posts`

---

## 2. Consultas MongoDB

A continuación se detallan las consultas a realizar en la base de datos, agrupadas por tipo de operación. Debajo de cada enunciado encontrará un espacio reservado para introducir los comandos utilizados.

---

### 2.1 INSERTAR DATOS

#### 📌 Insertar al menos 15 publicaciones nuevas con al menos 2 comentarios por publicación

Cada publicación debe contener:
- `username`
- `title`
- `body`
- `comments` (con al menos dos objetos que incluyan `username` y `body`)

```bash
load("posts.js")
```

---

#### 📌 Insertar al menos 10 nuevos usuarios

Cada usuario debe contener:
- `username`
- `email`
- `age`

```bash
load("users.js")
```

---

### 2.2 ACTUALIZAR DATOS


#### 📌 Actualiza todos los valores de los campos de una publicación

```bash
db.posts.updateOne(
  { title: "Mi primer patito de goma" }, // criterio de búsqueda
  {
    $set: {
      username: "nuevoUsuario",
      title: "Nuevo título actualizado",
      body: "Este es el nuevo contenido del cuerpo.",
      comments: [
        { username: "comentador1", body: "Primer comentario nuevo." },
        { username: "comentador2", body: "Segundo comentario nuevo." }
      ]
    }
  }
);

```

#### 📌 Cambia el valor del campo “body” de una publicación

```bash
db.posts.updateOne({ username: "gomaLover"}, {$set:{ body: "body cambiado en esta publicación"}})
```

#### 📌 Actualiza el comentario de una publicación

```bash
db.posts.updateOne({_id: ObjectId("6840338253a10f23a399490b"), "comments.username":"gomaLover"},{$set:{"comments.$.body":"¡Comentario actualizado!"}})
```

#### 📌 Actualiza todos los valores de los campos de un usuario

```bash
db.users.updateOne({username: "quackAttack"}, {$set: {username: "nuevoUsuario", email: "nuevoemail@mail.com", age: 35}})
```

#### 📌 Cambia el email de dos usuarios (hacer la consulta dos veces)

```bash
db.users.updateOne({username: "nuevoUsuario"}, {$set: {email: "otronuevomail@mail.com"}})

db.users.updateOne({username: "gomaLover"}, {$set: {email: "gomalovelovelover@mail.com"}})
```

#### 📌 Aumenta en 5 años la edad de un usuario

```bash
db.users.updateOne({username: "gomaLover"}, {$inc: { age: 5}})
```

---

### 2.3 OBTENER DATOS

#### 📌 Seleccionar todas las publicaciones

```bash
db.posts.find()
```

#### 📌 Selecciona las publicaciones que coincidan con el username indicado

```bash
db.posts.find({username: "gomaLover"})
```

#### 📌 Seleccione todos los usuarios con una edad mayor a 20

```bash
db.users.find({age:{$gt:20}})
```

#### 📌 Seleccione todos los usuarios con una edad inferior a 23

```bash
db.users.find({age:{$lt:23}})
```

#### 📌 Seleccione todos los usuarios con una edad entre 25 y 30 años

```bash
db.users.find({age:{$gte:25, $lte:30}})
```

#### 📌 Muestra los usuarios de edad menor a mayor

```bash
db.users.find().sort({age: 1})
```

#### 📌 Muestra los usuarios de edad mayor a menor

```bash
db.users.find().sort({age: -1})
```

#### 📌 Seleccione el número total de usuarios

```bash
db.users.find().count()
```

#### 📌 Seleccione todas las publicaciones y muéstralas con el siguiente formato:  
**Título de la publicación: "title one"**

```bash
db.posts.find().forEach(post => { print("Título de la publicación: "+ post.title)})
```

#### 📌 Selecciona solo 2 usuarios

```bash
db.users.find().limit(2)
```

#### 📌 Busca por title 2 publicaciones (hacer la misma consulta 2 veces)

```bash
db.posts.find({ title: "Día internacional del patito" })

db.posts.find({ title: "Día internacional del patito" })
```

---

### 2.4 BORRAR DATOS

#### 📌 Elimina a todos los usuarios con una edad mayor a 30

```bash
db.users.deleteMany({age:{$gt:30}})
```

---

## 3. Extra

#### 📌 Selecciona el número total de publicaciones que tienen más de un comentario

```bash
db.posts.countDocuments({$expr:{$gt:[{$size:"$comments"}, 1]}})
```

#### 📌 Selecciona la última publicación creada

```bash
db.posts.find().sort({_id: -1}).limit(1)
```

#### 📌 Selecciona 5 publicaciones que sean las últimas creadas

```bash
db.posts.find().sort({_id: -1}).limit(5)
```

#### 📌 Elimina todas las publicaciones que tengan más de un comentario

```bash
db.posts.deleteMany({$expr:{$gt: [{$size: "$comments"}, 1]}})
```

---
