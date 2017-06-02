---

layout: post
title: "(ETC) gitignore.io"
category: ETC

---

### 개요
[김태곤님의 블로그 글 중 신입 프론트엔드 개발자를 위한 면접 조언](https://taegon.kim/archives/5770)을 보다보면 그런 말이 나온다.
> .gitignore 파일에 .idea 폴더나 npm-debug.log 같은 불필요한 파일은 포함되지 않게 설정해두자. 코딩 능력과 상관없는 거지만 기본적인 사용법을 모르는 것처럼 보일 수 있다.

사실 핑계일지 모르지만 .gitignore을 개인 프로젝트 할 떄 신경을 덜 썼던건 사실이다..idea같은 폴더는 인텔리제이나 파이참 등에서 IDE를 쓸 때 환경 설정등이 들어가는 폴더라고 하는데 굳이 깃에는 올라갈 필요가 없는 폴더이기도 하다.

### 그럼?
그럼 어떤 파일은 gitignore를 하고 어떤 파일은 ignore할까? 이런 결정은 주로 내가 직접적으로 결정하는 파일이 아니면 대부분 동일한 것 같다.(이런 사이트가 있는 것을 보니)
<br/>

[이런 사이트가 있다,https://www.gitignore.io/](https://www.gitignore.io/). 우선 이 사이트는 원두님이 추천해 준 사이트이다. 이곳에는 사용하는 IDE, OS, Language를 입력하면 gitignore을 입력해준다. 지금 사용하고 있는 OS가 맥이고 python코딩을 pycharm에서 하고 있다고 가정하면!<br/><img src = '/post_img/201706/02/1.png'/>

```
# Created by https://www.gitignore.io/api/macos,python,pycharm

### macOS ###
*.DS_Store
.AppleDouble
.LSOverride

# Icon must end with two \r
Icon

# Thumbnails
._*

# Files that might appear in the root of a volume
.DocumentRevisions-V100
.fseventsd
.Spotlight-V100
.TemporaryItems
.Trashes
.VolumeIcon.icns
.com.apple.timemachine.donotpresent

# Directories potentially created on remote AFP share
.AppleDB
.AppleDesktop
Network Trash Folder
Temporary Items
.apdisk

### PyCharm ###
# Covers JetBrains IDEs: IntelliJ, RubyMine, PhpStorm, AppCode, PyCharm, CLion, Android Studio and Webstorm
# Reference: https://intellij-support.jetbrains.com/hc/en-us/articles/206544839

# User-specific stuff:
.idea/**/workspace.xml
.idea/**/tasks.xml
.idea/dictionaries

# Sensitive or high-churn files:
.idea/**/dataSources/
.idea/**/dataSources.ids
.idea/**/dataSources.xml
.idea/**/dataSources.local.xml
.idea/**/sqlDataSources.xml
.idea/**/dynamic.xml
.idea/**/uiDesigner.xml

# Gradle:
.idea/**/gradle.xml
.idea/**/libraries

# CMake
cmake-build-debug/

# Mongo Explorer plugin:
.idea/**/mongoSettings.xml

## File-based project format:
*.iws

## Plugin-specific files:

# IntelliJ
/out/

# mpeltonen/sbt-idea plugin
.idea_modules/

# JIRA plugin
atlassian-ide-plugin.xml

# Cursive Clojure plugin
.idea/replstate.xml

# Crashlytics plugin (for Android Studio and IntelliJ)
com_crashlytics_export_strings.xml
crashlytics.properties
crashlytics-build.properties
fabric.properties

### PyCharm Patch ###
# Comment Reason: https://github.com/joeblau/gitignore.io/issues/186#issuecomment-215987721

# *.iml
# modules.xml
# .idea/misc.xml
# *.ipr

# Sonarlint plugin
.idea/sonarlint

### Python ###
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
env/
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
*.egg-info/
.installed.cfg
*.egg

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
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*,cover
.hypothesis/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# pyenv
.python-version

# celery beat schedule file
celerybeat-schedule

# SageMath parsed files
*.sage.py

# dotenv
.env

# virtualenv
.venv
venv/
ENV/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# End of https://www.gitignore.io/api/macos,python,pycharm
```
이런 긴 ignore코드가 탄생한다. 이걸 .gitignore에 넣고 push!를 해주면 될 것 같다~


<br/><br/>