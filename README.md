# 📦 Proyecto con Pydantic  

Este proyecto utiliza [Pydantic](https://docs.pydantic.dev/) para **validar y manejar datos** de forma sencilla y robusta en Python 🚀.  

---

## 🛠️ Instalación  

Clona el repositorio y luego instala las dependencias:  

```
git clone https://github.com/tu-usuario/tu-repo.git
cd tu-repo
pip install -r requirements.txt
```

O bien, instala directamente Pydantic:
```
pip install pydantic
```

## 📖 Ejemplo de uso
Un ejemplo básico de validación de datos con **Pydantic**:

```
# Importamos lo necesario de Pydantic
from pydantic import BaseModel, EmailStr, Field

# Definimos un modelo de usuario que hereda de BaseModel
class User(BaseModel):
    # id debe ser un número entero
    id: int
    
    # name es un string obligatorio, con mínimo 3 y máximo 50 caracteres
    name: str = Field(..., min_length=3, max_length=50)
    
    # email debe tener formato válido de correo electrónico
    email: EmailStr
    
    # age debe ser un entero mayor o igual a 18
    age: int = Field(..., ge=18, description="Debe ser mayor de edad")

# ✅ Ejemplo con datos válidos
user = User(id=1, name="Juan", email="juan@example.com", age=20)
print(user)  # Muestra el objeto validado

# ❌ Ejemplo con datos inválidos (Pydantic lanza errores de validación)
try:
    User(id=2, name="A", email="no-es-email", age=15)
except Exception as e:
    print(e)  # Muestra los errores de validación
```

🔎 Explicación paso a paso

```BaseModel``` → Clase base de Pydantic para definir modelos de datos.

```Field(...)``` → Permite añadir reglas de validación como longitud mínima, máxima o rangos de números.

```EmailStr``` → Tipo especial que valida que el string sea un correo válido.

```Instanciar User(...)``` → Cuando creamos un objeto User, Pydantic automáticamente valida los datos.

```Errores de validación``` → Si los datos no cumplen las reglas, se generan mensajes detallados que indican el problema.

🔎 Salida esperada
```
id=1 name='Juan' email='juan@example.com' age=20

3 validation errors for User
name
  String should have at least 3 characters (type=value_error)
email
  value is not a valid email address (type=value_error.email)
age
  ensure this value is greater than or equal to 18 (type=value_error.number.not_ge)
```