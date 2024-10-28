## Base de datos nosql



Link al modelo

https://drive.google.com/file/d/14VkZQlPTaIbPImTKG9OkULUkIYqlGyPO/view?usp=sharing

### John Alejandro Gualteros

Usar base de datos

```bash
use toneodeportivo;
```


crear colecciones y insertar datos


#### Equipos

```bash
db.equipos.insertMany([
  { _id: ObjectId(), nombre: "Equipo A" },
  { _id: ObjectId(), nombre: "Equipo B" },
  { _id: ObjectId(), nombre: "Equipo C" }
])
```

#### Deportistas

```bash
db.deportistas.insertMany([
  { _id: ObjectId(), nombre: "Juan Pérez", edad: 24, equipo: ObjectId("ID_EQUIPO_A"), posicion: "atacante", documento: "12345678" },
  { _id: ObjectId(), nombre: "Luis Gómez", edad: 27, equipo: ObjectId("ID_EQUIPO_B"), posicion: "defensa", documento: "87654321" },
  { _id: ObjectId(), nombre: "Ana Rodríguez", edad: 21, equipo: ObjectId("ID_EQUIPO_A"), posicion: "centrocampista", documento: "11223344" }
])
```

#### Entrenadores

```bash
db.entrenadores.insertMany([
  { _id: ObjectId("652f1e8f0e0a52c4c12a904"), nombre: "Carlos López", experiencia: 10, equipo: ObjectId("652e8e8f0e0a52c4c12a912"), especializacion: "estrategia de juego" },
  { _id: ObjectId("652f1e8f0e0a52c4c12a905"), nombre: "María Torres", experiencia: 5, equipo: ObjectId("652e8e8f0e0a52c4c12a913"), especializacion: "entrenamiento físico" }
])
```


#### Arbitros

```bash
db.arbitros.insertMany([
  { _id: ObjectId(), nombre: "Pedro Sánchez", experiencia: 15, encuentros_asignados: [ObjectId("ID_ENCUENTRO_1"), ObjectId("ID_ENCUENTRO_2")] },
  { _id: ObjectId(), nombre: "Laura Díaz", experiencia: 8, encuentros_asignados: [ObjectId("ID_ENCUENTRO_3")] }
])
```

#### Encuentros deportivos

```bash
db.encuentros_deportivos.insertMany([
  { _id: ObjectId(), fecha: new Date("2024-11-10T14:00:00Z"), lugar: "Estadio Central", equipos_participantes: [ObjectId("ID_EQUIPO_A"), ObjectId("ID_EQUIPO_B")], arbitro: ObjectId("ID_ARBITRO_1") },
  { _id: ObjectId(), fecha: new Date("2024-11-12T16:00:00Z"), lugar: "Estadio Norte", equipos_participantes: [ObjectId("ID_EQUIPO_A"), ObjectId("ID_EQUIPO_C")], arbitro: ObjectId("ID_ARBITRO_2") }
])
```

#### Resultados
    
```bash
db.resultados.insertMany([
  { _id: ObjectId(), ganador: ObjectId("ID_EQUIPO_A"), perdedor: ObjectId("ID_EQUIPO_B"), resultado: "2-1", encuentro: ObjectId("ID_ENCUENTRO_1") },
  { _id: ObjectId(), ganador: "draw", perdedor: "draw", resultado: "1-1", encuentro: ObjectId("ID_ENCUENTRO_2") }
])
```


#### Posiciones

```bash
db.posiciones.insertMany([
  { _id: ObjectId(), posicion: 1, equipo: ObjectId("ID_EQUIPO_A"), puntos: 25, temporada: "2024" },
  { _id: ObjectId(), posicion: 2, equipo: ObjectId("ID_EQUIPO_B"), puntos: 20, temporada: "2024" },
  { _id: ObjectId(), posicion: 3, equipo: ObjectId("ID_EQUIPO_C"), puntos: 18, temporada: "2024" }
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