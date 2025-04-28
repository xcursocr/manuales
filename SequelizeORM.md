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

🛠 13. Búsquedas Dinámicas (LIKE)
💡 Buscar por nombre, descripción o cualquier campo de texto.

```js
import { Op } from 'sequelize';

export const searchProducts = async (req, res) => {
  const { q } = req.query;

  const products = await Product.findAll({
    where: {
      nombre: {
        [Op.like]: `%${q}%`
      }
    },
    include: [
      { model: Category, as: "category" },
      { model: Image, as: "images" }
    ],
    order: [["nombre", "ASC"]]
  });

  res.render("admin/products/search", {
    title: "Buscar Productos",
    products,
    q
  });
};

```
📊 14. Reporte de Conteos por Categoría (Agrupaciones GROUP BY)
💡 Saber cuántos productos tiene cada categoría.
💬 sequelize.fn() permite usar funciones de SQL como COUNT, SUM, AVG, etc.
```js
import { sequelize } from "../config/database.js";

export const countProductsByCategory = async (req, res) => {
  const results = await Product.findAll({
    attributes: [
      "categoryId",
      [sequelize.fn("COUNT", sequelize.col("id")), "totalProductos"]
    ],
    group: ["categoryId"],
    include: [{ model: Category, as: "category" }]
  });

  res.json(results);
};

```
🔗 15. Filtros por Parámetros de URL
💡 Listar productos por categoría, rango de precios, o estado.

```js
import { Op } from 'sequelize';

export const filterProducts = async (req, res) => {
  const { minPrice, maxPrice, categoryId } = req.query;

  const products = await Product.findAll({
    where: {
      ...(categoryId && { categoryId }),
      ...(minPrice && maxPrice && {
        precio: {
          [Op.between]: [minPrice, maxPrice]
        }
      })
    },
    include: [
      { model: Category, as: "category" },
      { model: Image, as: "images" }
    ],
    order: [["precio", "ASC"]]
  });

  res.render("admin/products/filter", {
    title: "Filtrar Productos",
    products
  });
};

```
🔥 16. Múltiples Relaciones Anidadas (Multi-Join)
💡 Traer usuario, sus posts, y los comentarios de esos posts.
💬 Puedes anidar include tantas veces como necesites, según las relaciones.
```js
const usuarios = await Usuario.findAll({
  include: [{
    model: Post,
    as: "posts",
    include: [{
      model: Comment,
      as: "comments"
    }]
  }]
});

```
🎯 17. Subconsultas Manuales (SubQuery)
💡 Consultar el primer producto más barato de cada categoría (requiere SQL más complejo, usando Sequelize o RAW SQL).

Ejemplo usando Sequelize:
💬 sequelize.literal() permite usar SQL crudo donde Sequelize no puede construirlo solo.
```js
const productos = await Product.findAll({
  where: {
    precio: {
      [Op.lte]: sequelize.literal(`(
        SELECT MIN(precio)
        FROM products AS p2
        WHERE p2.categoryId = products.categoryId
      )`)
    }
  },
  include: [{ model: Category, as: "category" }]
});

```
🚀 18. Orden Dinámico desde la Vista
💡 Permitir que el usuario ordene (por precio, fecha, nombre).
Ejemplo de URLs para probar:

/productos?sortBy=precio&sortDir=ASC

/productos?sortBy=nombre&sortDir=DESC
```js
export const listProducts = async (req, res) => {
  const { sortBy = "createdAt", sortDir = "DESC" } = req.query;

  const products = await Product.findAll({
    order: [[sortBy, sortDir]],
    include: [
      { model: Category, as: "category" },
      { model: Image, as: "images" }
    ]
  });

  res.render("admin/products/index", {
    title: "Productos",
    products
  });
};

```
 Resumen Final de Consultas Avanzadas

Técnica	Uso práctico
LIKE	Buscadores en tiempo real
findAndCountAll + Paginación	Listados paginados
Group by + Count/Sum	Reportes, dashboard
Filtros dinámicos (URL)	Catálogos filtrables
Relaciones anidadas	Cargar varias tablas juntas
Subconsultas	Datos más complejos
Orden dinámico (sortBy)	Tablas ordenables en frontend

## 🧠 Buenas Prácticas

- Usa `async/await` para todo.
- Declara tus relaciones antes de sincronizar.
- No uses `force: true` en producción.
- Usa `Op` de Sequelize para condiciones complejas.
- Agrupa lógica de BD en métodos del modelo o servicios.

---

¿Quieres que prepare ahora la guía para **migraciones, seeders y relaciones avanzadas** en Sequelize o seguimos con otro tema?
