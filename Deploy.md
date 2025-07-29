# DEPLOY

### KOYEB

Comentar la linea de codigo
```python
# load_dotenv()
```

```python
BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.environ.get("SECRET_KEY", "clave-insegura")
DEBUG = os.environ.get("DEBUG", "False") == "True"

# Agregale la url que se genera en koyeb
ALLOWED_HOSTS = [
    "", # Agregar una vez hecho deploy 
    "localhost",
    "127.0.0.1",
]

# Añadir el MIDDLWARE de "whitenoise.middleware.WhiteNoiseMiddleware",
MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware", #Añadir
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
    "social_django.middleware.SocialAuthExceptionMiddleware",
]

ROOT_URLCONF = "backend.urls"


## Añadir los dos siguientes processors
TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [BASE_DIR / "templates"],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
                "social_django.context_processors.backends", # Añadir 
                "social_django.context_processors.login_redirect", # Añadir
            ],
        },
    },
]

# Configuración de Google OAuth2
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = os.environ.get('GOOGLE_OAUTH2_KEY')
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = os.environ.get('GOOGLE_OAUTH2_SECRET')

# URLs de redirección después del login
LOGIN_URL = "login"
LOGIN_REDIRECT_URL = "profile"
LOGOUT_URL = "index"
LOGOUT_REDIRECT_URL = "index"


# Añadir la siguiente linea para archivos estativos
STATIC_URL = "/static/"
STATICFILES_DIRS = [BASE_DIR / "static"]
STATIC_ROOT = BASE_DIR / "staticfiles" # Añadir

```

En koyeb configurar variables globales

```
DEBUG = FALSE
GOOGLE_OAUTH2_KEY= ID de cliente
GOOGLE_OAUTH2_SECRET= Secreto del cliente
SECRET_KEY = clave secreta
```

Antes de hacer deploy 
```
python3 manage.py collectstatic --noinput
```
En koyeb
python3 manage.py makemigrations
python3 manage.py migrate




