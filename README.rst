=====
GovBR Login
=====

GovBR Login is a Django app to connect your system with GovBR social account. With this app,
you can provide a way for users login using GovBR credentials.

Detailed documentation is in the "docs" directory.

Quick start
-----------

1. Add "allauth" and "govbr_login" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = [
        # The following apps are required:
        'django.contrib.auth',
        'django.contrib.messages',
        ...
        'allauth',
        'allauth.account',
        'allauth.socialaccount',
        'allauth.socialaccount.providers.openid_connect',
        'govbr_login',
    ]

    # Visit https://docs.allauth.org/en/latest/installation/quickstart.html#quickstart for more details

2. Configure django middleware and authentication backend with allauth requirements in your setings like this::

    MIDDLEWARE = (
        'django.middleware.common.CommonMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',

        'allauth.account.middleware.AccountMiddleware',
    )

    AUTHENTICATION_BACKENDS = [
        'django.contrib.auth.backends.ModelBackend',
        'allauth.account.auth_backends.AuthenticationBackend',
    ]

    # Visit https://docs.allauth.org/en/latest/installation/quickstart.html#post-installation for more details

3. Include GovBr domain (staging or production) and paths to login services in your setings like this::

    # GovBR client config
    SOCIALACCOUNT_GOVBR_SSO_DOMAIN = "https://sso.staging.acesso.gov.br"
    SOCIALACCOUNT_GOVBR_AUTHORIZATION_PATH = "/authorize"
    SOCIALACCOUNT_GOVBR_ACCESS_TOKEN_PATH = "/token"
    SOCIALACCOUNT_GOVBR_USER_INFO_PATH = "/userinfo"

    # Visit GovBr tutorial (https://manual-roteiro-integracao-login-unico.servicos.gov.br/pt/stable/iniciarintegracao.html)
    # for more details about required domain and paths

4. Run ``python manage.py migrate`` to create the allauth dependency models.

5. Start the development server and visit http://127.0.0.1:8000/admin/ (you'll need the Admin app enabled) to:

   1. replace 'example.com' site with your url site;
   2. create a SocialApp with GovBr Provider and your url site defined in previous step.

 See tutorial to know how to request client_id and secret_id: https://manual-roteiro-integracao-login-unico.servicos.gov.br/pt/stable/solicitarconfiguracao.html

6. Visit http://127.0.0.1:8000/accounts/govbr/login/ to use your govbr login.
