# PythonAnywhere 배포하기

## 1. `.gitignore` 파일

- 프로젝트의 최상위 폴더에 `.gitignore`이라는 파일을 만들어서 아래의 내용을 복사함

```
# Created by https://www.toptal.com/developers/gitignore/api/django
# Edit at https://www.toptal.com/developers/gitignore?templates=django

### Django ###
*.log
*.pot
*.pyc
__pycache__/
local_settings.py
db.sqlite3
db.sqlite3-journal
media
.idea/

# If your build process includes running collectstatic, then you probably don't need or want to include staticfiles/
# in your Git repository. Update and uncomment the following line accordingly.
# <django-project-name>/staticfiles/

### Django.Python Stack ###
# Byte-compiled / optimized / DLL files
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
pip-wheel-metadata/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/
pytestdebug.log

# Translations
*.mo

# Django stuff:

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/
doc/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
.python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.
#Pipfile.lock

# PEP 582; used by e.g. github.com/David-OConnor/pyflow
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/

# pytype static type analyzer
.pytype/

# End of https://www.toptal.com/developers/gitignore/api/django
```



## 2. 프로젝트 사항 변경

### 1) `settings.py` 내용 변경 <!-- {docsify-ignore} -->

- 프로젝트 `settings.py` 내용 중 해당되는 부분의 코드를 아래처럼 변경해줌

```python
DEBUG = False

ALLOWED_HOSTS = ['*']

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

### 2) `static` 폴더 생성 <!-- {docsify-ignore} -->

- 상위 폴더에 빈 `static` 폴더 생성
  - `pythonanywhere`에서 정적 파일 모을 때 사용하는 용도



## 3. `requirements.txt` 파일 

- 파이썬 모듈과 버전을 유지할 수 있는 파일을 생성하는 과정
- 파이참의 터미널 창에서 아래 명령에 수행

```django
pip freeze > requirements.txt
```



## 4. `GitHub의 repository`에 프로젝트 올리기



## 5. `PythonAnywhere`로 코드 가져오기

- 파이썬애니웨어의 대시보드에서 'Bash' 콘솔의 옵션을 선택함
- Bash 콘솔 창에 아래와 같이 입력함

```bash
$ git clone [github에서 생성한 원격저장소 주소] [PythonAnywhere에서 사용할 폴더 이름]
```



## 6. `PythonAnywhere`에 `가상환경` 생성하기

- 파이썬애니웨어 상에서 사용할 가상환경을 생성함
- Bash 콘솔 창에 아래와 같이 입력함

```bash
$ mkvirtualenv [가상환경 이름] --python=python3.7
```

- 파이썬 버전은 자신이 개발할 때 사용한 버전과 동일하게 입력하면 됨

#### + 가상환경 활성화 / 비활성화

- `deactivate` 는 가상환경 비활성화 명령어
- `workon`은 가상환경 활성화 명령어

```bash
(가상환경 이름) $ deactivate
$  which python
/usr/bin/python

$  workon [가상환경 이름]
(가상환경 이름) $ which python
/home/[파이썬애니웨어 아이디]/.virtualenvs/[가상환경 이름]/bin/python
```



## 7. `PythonAnywhere`에 `Django` 설치

```bash
$ pip install django
```



## 8. `PythonAnywhere`에 `Database` 생성

- 로컬 컴퓨터와 서버에는 차이가 있으므로 데이터베이스를 초기화해주는 단계가 필요함
- 가상 환경이 활성화된 상태인지 확인하고 명령어를 실행해야함

```bash
(가상환경 이름) $ python manage.py migrate
```

#### + superuser 생성

```bash
(가상환경 이름) $ python manage.py createsuperuser
```



## 9. 정적 파일 모으기

- 모든 정적파일을 모아서 서버가 찾을 수 있는 자옷에 모아둬야 함
- 프로젝트 최상위폴더에 `static` 폴더가 존재해야 오류가 발생하지 않음
- 가상 환경이 활성화된 상태인지 확인해야 함

```bash
(가상환경 이름) $ python manage.py collectstatic
```



## 10. 웹 앱으로 배포하기

- 파이썬애니웨어의 대시보드에서 `Web` 탭으로 들어 간 후 `Add a new web app` 을 클릭함
- 수동 설정**(manual configuration)** 을 선택한 후, 알맞은 파이썬 버전을 선택함



### 1) 가상환경 설정 <!-- {docsify-ignore} -->

- `Virtualenv:` 부분에 가서 가상환경 경로를 입력함
- /home/[파이썬애니웨어 아이디]/.virtualenvs/[가상환경 이름]
- 경로를 잘 못 설정하면 오류 메세지 띄워주므로 참고해서 변경



### 2) 정적 파일 매핑하기 <!-- {docsify-ignore} -->

- `Static files:` 부분에 가서 정적파일 경로 입력하기

- `Enter URL` 이라는 빨간색 텍스트를 클릭하고 `/static/`을 입력함

- 그 옆의 `Enter path`라는 빨간색 텍스트를 클릭하고 

  `/home/[파이썬애니웨어 아이디]/[클론받은 프로젝트 있는 폴더 이름]/static` 을 입력함



### 3) WSGI 파일 설정하기 <!-- {docsify-ignore} -->

- `Code:` 부분의 `WSGI configuration file`로 지정되어 있는 파일을 클릭해서 에디터를 실행
- 모든 내용을 지우고 아래의 내용으로 변경함
- `path`의 내용과 `os.environ` 의 내용은 적절하게 변경해줘야 함

```python
import os
import sys

path = '/home/[파이썬애니웨어 아이디]/[클론받은 프로젝트 있는 폴더 이름]'
if path not in sys.path:
    sys.path.append(path)

from django.contrib.staticfiles.handlers import StaticFilesHandler
from django.core.wsgi import get_wsgi_application

os.environ['DJANGO_SETTINGS_MODULE'] = '[프로젝트이름].settings'
# 대부분 프로젝트 이름이지만 헷갈린다면 프로젝트의 wsgi.py 내용을 복사해서 붙여넣은 다음
# 변경해야할 부분 변경해주면 됨
application = StaticFilesHandler(get_wsgi_application())
```

- 내용을 변경한 후 `save`를 클릭하고 `Web` 탭으로 돌아감
- `Web` 탭 상단의 `Reload:` 부분의 초록색 버튼을 클릭한 후, 웹 애플리케이션으로 들어가 봄



