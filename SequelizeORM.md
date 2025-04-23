# 🐘 Sequelize: Guía Completa para Consultas y Modelos  
> ORM = Object-Relational Mapping → Traduce datos de una BD a objetos JS

---

## 🧱 1. Definir un Modelo  
💡 Usamos clases modernas. Cada modelo representa una tabla.

```js
// models/Usuario.js
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database.js';

class Usuario extends Model {}

Usuario.init({
  nombre: DataTypes.STRING,
  email: DataTypes.STRING,
  edad: DataTypes.INTEGER,
}, {
  sequelize,
  modelName: 'Usuario',
  tableName: 'usuarios',
  timestamps: false,
});

export default Usuario;
```

---

## 📥 2. Insertar Registros  
💡 `.create()` inserta un nuevo registro. Retorna el objeto creado.

```js
await Usuario.create({
  nombre: 'Carlos',
  email: 'carlos@mail.com',
  edad: 30,
});
```

---

## 🔍 3. Consultar Registros (SELECT)

### 🔹 Todos  
```js
const usuarios = await Usuario.findAll();
```

### 🔹 Con condiciones (`WHERE`)  
```js
import { Op } from 'sequelize';

const adultos = await Usuario.findAll({
  where: {
    edad: { [Op.gte]: 18 }
  }
});
```

### 🔹 Uno solo  
```js
const usuario = await Usuario.findOne({
  where: { nombre: 'Carlos' }
});
```

### 🔹 Por ID  
```js
const usuario = await Usuario.findByPk(1);
```

---

## ✏️ 4. Actualizar Registros  
💡 `.update()` actualiza según condiciones.

```js
await Usuario.update(
  { edad: 35 },
  { where: { id: 1 } }
);
```

---

## ❌ 5. Eliminar Registros  
💡 `.destroy()` elimina registros que cumplan una condición.

```js
await Usuario.destroy({
  where: { id: 1 }
});
```

---

## 🔄 6. Relaciones entre Modelos

### 🔹 Uno a Muchos (1:N)  
```js
Usuario.hasMany(Post, { foreignKey: 'usuarioId' });
Post.belongsTo(Usuario, { foreignKey: 'usuarioId' });
```

### 🔹 Muchos a Muchos (N:N)  
```js
Usuario.belongsToMany(Rol, { through: 'usuario_rol' });
Rol.belongsToMany(Usuario, { through: 'usuario_rol' });
```

---

## 🔗 7. JOIN: Incluir Relaciones  
💡 `.include` se usa para traer datos relacionados.

```js
const usuarios = await Usuario.findAll({
  include: Post
});
```

---

## 📦 8. Paginación (LIMIT + OFFSET)  
💡 Muy útil para paginar resultados en listas.

```js
const page = 2;
const limit = 10;

const usuarios = await Usuario.findAll({
  offset: (page - 1) * limit,
  limit
});
```

---

## ✅ 9. Validaciones y Valores por Defecto

```js
edad: {
  type: DataTypes.INTEGER,
  allowNull: false,
  defaultValue: 18,
  validate: {
    min: 1,
    max: 120
  }
}
```

---

## 🧠 10. Métodos Personalizados  
💡 Puedes agregar funciones útiles a tus modelos.

```js
Usuario.prototype.saludo = function () {
  return `Hola, soy ${this.nombre}`;
};
```

---

## 🧩 11. Sincronizar Modelos con la BD  
💡 `.sync()` crea las tablas si no existen.

```js
await sequelize.sync();
await sequelize.sync({ force: true }); // cuidado: borra y recrea todo
```

---
🧠 12. Consulta Compleja con Paginación, Relaciones y Ordenamiento
💡 Ideal para paneles de administración o dashboards. Combina findAndCountAll con relaciones y orden.

```js
export const listProducts = async (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limitPage = 10;
  const offset = (page - 1) * limitPage;

  // Trae productos con sus categorías e imágenes
  const { count, rows: products } = await Product.findAndCountAll({
    include: [
      { model: Category, as: "category" },
      { model: Image, as: "images" }
    ],
    limit: limitPage,
    offset: offset,
    order: [["createdAt", "DESC"]]
  });

  const totalPages = Math.ceil(count / limitPage);

  res.render("admin/products/index", {
    title: "Productos",
    products,
    page,
    totalPages
  });
};

```

🔍 Explicación Rápida
findAndCountAll: útil para paginar porque devuelve count total y rows (datos actuales).

include: carga las relaciones definidas (con as si usaste alias).

order: ordena por campo (createdAt descendente).

limit y offset: necesarios para paginación.

res.render(...): renderiza con EJS o cualquier motor de plantillas.

🎓 Tips Avanzados
Si tienes filtros dinámicos (por ejemplo, por categoría), puedes agregarlos a where.

```js
where: {
  ...(req.query.category && { categoryId: req.query.category })
}

```

. Puedes hacer búsquedas (LIKE) con Sequelize fácilmente:

```js
where: {
  nombre: {
    [Op.like]: `%${req.query.q}%`
  }
}

```
. Para ordenar dinámicamente:
```js
order: [[req.query.sort || 'createdAt', req.query.dir || 'DESC']]

```

## 🧠 Buenas Prácticas

- Usa `async/await` para todo.
- Declara tus relaciones antes de sincronizar.
- No uses `force: true` en producción.
- Usa `Op` de Sequelize para condiciones complejas.
- Agrupa lógica de BD en métodos del modelo o servicios.

---

¿Quieres que prepare ahora la guía para **migraciones, seeders y relaciones avanzadas** en Sequelize o seguimos con otro tema?
