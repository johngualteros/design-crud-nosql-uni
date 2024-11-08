## Base de datos nosql



Link al modelo

https://drive.google.com/file/d/14VkZQlPTaIbPImTKG9OkULUkIYqlGyPO/view?usp=sharing

### John Alejandro Gualteros

## Creación de la Base de Datos

Para crear la base de datos, ejecute el siguiente comando en la terminal de MongoDB:

```bash
use base_deportiva
```

## Creación de Colecciones y Datos de Ejemplo

### Colección: `deportistas`

```bash
db.deportistas.insertMany([
  {
    _id: ObjectId(),
    nombre: "Carlos Pérez",
    edad: 24,
    equipo: ObjectId("6484f743bcf86cd799d7a12f"),
    posicion: "Delantero",
    documento: "123456789"
  },
  {
    _id: ObjectId(),
    nombre: "Ana Gómez",
    edad: 28,
    equipo: ObjectId("6484f743bcf86cd799d7a130"),
    posicion: "Defensa",
    documento: "987654321"
  }
])
```

### Colección: `equipos`

```bash
db.equipos.insertMany([
  {
    _id: ObjectId("6484f743bcf86cd799d7a12f"),
    nombre: "Tigres FC"
  },
  {
    _id: ObjectId("6484f743bcf86cd799d7a130"),
    nombre: "Leones FC"
  }
])
```

### Colección: `entrenadores`

```bash
db.entrenadores.insertMany([
  {
    _id: ObjectId(),
    nombre: "Juan López",
    equipo: ObjectId("6484f743bcf86cd799d7a12f"),
    experiencia: 10,
    especializacion: "Física"
  },
  {
    _id: ObjectId(),
    nombre: "Maria Martinez",
    equipo: ObjectId("6484f743bcf86cd799d7a130"),
    experiencia: 8,
    especializacion: "Táctica"
  }
])
```

### Colección: `arbitros`

```bash
db.arbitros.insertMany([
  {
    _id: ObjectId(),
    nombre: "Pedro Jiménez",
    encuentros_asignados: [ObjectId("6484f743bcf86cd799d7a132")]
  },
  {
    _id: ObjectId(),
    nombre: "Luis Herrera",
    encuentros_asignados: [ObjectId("6484f743bcf86cd799d7a133")]
  }
])
```

### Colección: `posiciones`

```bash
db.posiciones.insertMany([
  {
    _id: ObjectId(),
    posicion: 1,
    equipo: ObjectId("6484f743bcf86cd799d7a12f"),
    puntos: 30,
    temporada: "2024"
  },
  {
    _id: ObjectId(),
    posicion: 2,
    equipo: ObjectId("6484f743bcf86cd799d7a130"),
    puntos: 28,
    temporada: "2024"
  }
])
```

### Colección: `encuentros_deportivos`

```bash
db.encuentros_deportivos.insertMany([
  {
    _id: ObjectId("6484f743bcf86cd799d7a132"),
    fecha: new Date("2024-11-08"),
    lugar: "Estadio Nacional",
    equipos_participantes: [ObjectId("6484f743bcf86cd799d7a12f"), ObjectId("6484f743bcf86cd799d7a130")],
    arbitro: ObjectId("6484f743bcf86cd799d7a134")
  },
  {
    _id: ObjectId("6484f743bcf86cd799d7a133"),
    fecha: new Date("2024-11-15"),
    lugar: "Arena Coliseo",
    equipos_participantes: [ObjectId("6484f743bcf86cd799d7a130"), ObjectId("6484f743bcf86cd799d7a12f")],
    arbitro: ObjectId("6484f743bcf86cd799d7a135")
  }
])
```

### Colección: `resultados`

```bash
db.resultados.insertMany([
  {
    _id: ObjectId(),
    ganador: ObjectId("6484f743bcf86cd799d7a12f"),
    perdedor: ObjectId("6484f743bcf86cd799d7a130"),
    resultado: "3-1",
    encuentro: ObjectId("6484f743bcf86cd799d7a132")
  },
  {
    _id: ObjectId(),
    ganador: ObjectId("6484f743bcf86cd799d7a130"),
    perdedor: ObjectId("6484f743bcf86cd799d7a12f"),
    resultado: "2-0",
    encuentro: ObjectId("6484f743bcf86cd799d7a133")
  }
])
```

Mostrar colecciones

```bash
show collections;
```

Mostrar datos de una colección

```bash
db.equipos.find().pretty();
```

query para ver todos los deportistas que pertenecen al equipo "Tigres FC".

```bash
db.deportistas.find({ equipo: ObjectId("6484f743bcf86cd799d7a12f") })
```

### 2. Consultar los entrenadores con más de 5 años de experiencia

```bash
db.entrenadores.find({ experiencia: { $gt: 5 } })
```

### 3. Ver todos los encuentros deportivos de un equipo en particular

```bash
db.encuentros_deportivos.find({ equipos_participantes: ObjectId("6484f743bcf86cd799d7a130") })
```

### 4. Obtener el ranking de equipos según sus puntos en una temporada

```bash
db.posiciones.find({ temporada: "2024" }).sort({ puntos: -1 })
```

### 5. Buscar el resultado de un encuentro específico

```bash
db.resultados.find({ encuentro: ObjectId("6484f743bcf86cd799d7a132") })
```

### 6. Contar el número de encuentros asignados a un árbitro específico

```bash
db.arbitros.aggregate([
  { $match: { nombre: "Pedro Jiménez" } },
  { $project: { numero_encuentros: { $size: "$encuentros_asignados" } } }
])
```

### 7. Obtener todos los detalles de los encuentros en una fecha específica

```bash
db.encuentros_deportivos.find({ fecha: new Date("2024-11-08") })
```

### 8. Buscar todos los equipos entrenados por un entrenador específico

```bash
db.entrenadores.find({ nombre: "Maria Martinez" }, { equipo: 1, _id: 0 })
```

### 9. Obtener la lista de equipos y sus posiciones en la temporada 2024

```bash
db.equipos.aggregate([
  {
    $lookup: {
      from: "posiciones",
      localField: "_id",
      foreignField: "equipo",
      as: "posiciones"
    }
  },
  { $unwind: "$posiciones" },
  { $match: { "posiciones.temporada": "2024" } },
  { $project: { nombre: 1, "posiciones.posicion": 1, "posiciones.puntos": 1 } }
])
```

### 10. Consultar todos los encuentros donde un equipo específico ganó

```bash
db.resultados.find({ ganador: ObjectId("6484f743bcf86cd799d7a12f") })
