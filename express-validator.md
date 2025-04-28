```js
// Express Validator - Tutorial Completo

// Introducción

// express-validator es una biblioteca para validar y sanitizar datos en las peticiones HTTP en aplicaciones Express.js.
// Se integra fácilmente en los middlewares para validar datos antes de llegar a los controladores.

// Instalación

// Ejecutar en la terminal:
/// npm install express-validator

// Requerir en tu proyecto:
import { body, validationResult, param, query } from 'express-validator';

// Uso Básico

// Validar que el campo "nombre" no esté vacío y que el campo "email" tenga formato válido.

import express from 'express';
const app = express();
app.use(express.json()); // Para parsear JSON

app.post('/registro', [
    body('nombre').notEmpty().withMessage('El nombre es obligatorio'),
    body('email').isEmail().withMessage('Debe ser un email válido')
], (req, res) => {
    const errores = validationResult(req);
    if (!errores.isEmpty()) {
        return res.status(400).json({ errores: errores.array() });
    }
    res.send('Registro exitoso');
});

// Explicación:
// - `body('nombre')`: Se refiere a los datos del cuerpo de la solicitud.
// - `.notEmpty()`: Valida que no esté vacío.
// - `.isEmail()`: Valida que sea un correo electrónico correcto.
// - `validationResult(req)`: Extrae los errores de la validación.

// Validaciones Comunes

// 1. Validar campos de tipo String

body('usuario')
    .isString().withMessage('Debe ser un texto')
    .isLength({ min: 3, max: 20 }).withMessage('Debe tener entre 3 y 20 caracteres');

// 2. Validar campos numéricos

body('edad')
    .isInt({ min: 18, max: 99 }).withMessage('Debe ser un número entre 18 y 99');

// 3. Validar campos booleanos

body('acepta')
    .isBoolean().withMessage('Debe ser verdadero o falso');

// 4. Validar fechas

body('fechaNacimiento')
    .isISO8601().toDate().withMessage('Debe ser una fecha válida');

// 5. Validar valores específicos

body('rol')
    .isIn(['admin', 'user', 'guest']).withMessage('Rol inválido');

// Sanitización de Datos

// Además de validar, express-validator permite sanitizar (limpiar) datos.

// 1. Trim: Eliminar espacios al principio y final

body('nombre').trim();

// 2. Escape: Escapar caracteres peligrosos

body('comentario').escape();

// 3. Normalizar Email

body('email').normalizeEmail();

// Validar Parámetros en URL

// Usamos `param` para validar parámetros dinámicos de rutas.

app.get('/usuario/:id', [
    param('id').isInt().withMessage('El ID debe ser un número')
], (req, res) => {
    const errores = validationResult(req);
    if (!errores.isEmpty()) {
        return res.status(400).json({ errores: errores.array() });
    }
    res.send(`Usuario ID: ${req.params.id}`);
});

// Validar Query Params

// Usamos `query` para validar parámetros en la URL después del signo `?`.

app.get('/buscar', [
    query('nombre').notEmpty().withMessage('El nombre es obligatorio')
], (req, res) => {
    const errores = validationResult(req);
    if (!errores.isEmpty()) {
        return res.status(400).json({ errores: errores.array() });
    }
    res.send(`Buscando: ${req.query.nombre}`);
});

// Personalizar Mensajes de Error

// Puedes encadenar `.withMessage('mensaje')` después de cada regla.

body('email')
    .isEmail()
    .withMessage('Debe ingresar un email válido');

// Validar campos anidados (objetos o arrays)

// Si recibimos un objeto como:
// {
//   "usuario": { "nombre": "Juan", "edad": 30 }
// }

body('usuario.nombre')
    .notEmpty().withMessage('El nombre de usuario es obligatorio');

body('usuario.edad')
    .isInt().withMessage('La edad debe ser un número');

// Validar listas o arrays

// Para validar cada elemento de un array:

body('etiquetas')
    .isArray().withMessage('Las etiquetas deben ser un array');

body('etiquetas.*')
    .isString().withMessage('Cada etiqueta debe ser un texto');

// Middleware para centralizar validaciones

// Podemos hacer un middleware para no repetir el mismo código en todas las rutas.

const validarCampos = (req, res, next) => {
    const errores = validationResult(req);
    if (!errores.isEmpty()) {
        return res.status(400).json({ errores: errores.array() });
    }
    next();
};

// Luego, usarlo después de los validators:

app.post('/producto', [
    body('nombre').notEmpty(),
    body('precio').isFloat({ gt: 0 })
], validarCampos, (req, res) => {
    res.send('Producto creado');
});

// Validación Condicional

// A veces queremos validar un campo sólo si otro campo existe o tiene un valor específico.

body('descuento')
    .if(body('esPromocion').equals('true'))
    .isFloat({ min: 0, max: 100 })
    .withMessage('El descuento debe ser un número entre 0 y 100');

// Custom Validators (Validadores personalizados)

// Podemos crear validadores propios.

body('password')
    .custom((valor, { req }) => {
        if (valor !== req.body.confirmPassword) {
            throw new Error('Las contraseñas no coinciden');
        }
        return true;
    });

// Agrupar Validaciones

// Puedes crear funciones que agrupen validaciones para reutilizarlas.

const validarRegistro = [
    body('nombre').notEmpty().withMessage('El nombre es obligatorio'),
    body('email').isEmail().withMessage('Debe ser un email válido'),
    body('password').isLength({ min: 6 }).withMessage('La contraseña debe tener mínimo 6 caracteres')
];

app.post('/nuevo-usuario', validarRegistro, validarCampos, (req, res) => {
    res.send('Usuario registrado');
});

// Buenas Prácticas

// - Siempre sanitizar los inputs además de validarlos.
// - Crear middlewares de validación reutilizables.
// - Personalizar los mensajes de error de forma clara para el usuario.
// - Validar tanto en el cliente como en el servidor (defensa en profundidad).

// Conclusión Final

// express-validator es una herramienta esencial para aplicaciones Express modernas, 
// permite asegurar que los datos que recibimos son correctos, seguros y limpios, reduciendo errores y aumentando la seguridad de las aplicaciones.
