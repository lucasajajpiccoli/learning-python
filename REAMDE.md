# Python

<br>

## Execução em linha de comando

<br>

### Execução de arquivos

<br>

`python [-bBdEhiIOPqRsSuvVWx?] [-c command | -m module-name | script | - ] [args]`
	
- No `--help` consta como `python3 [option] ... [-c cmd | -m mod | file | -] [arg] ...`
  - `<script>` deve ser o nome do arquivo mesmo
- > Execute the Python code contained in script, which must be a filesystem path (absolute or relative) referring to either a Python file, a directory containing a `__main__.py` file, or a zipfile containing a `__main__.py` file.

<br>

### Scripts executáveis

<br>

Pode-se inserir `#!/usr/bin/env python3` como primeira linha do documento

Pode-se também mudar as permissões do arquivo com `chmod +x myscript.py`

<br>

## Módulos e pacotes

<br>

> A module is a file containing Python definitions and statements. The file name is the module name with the suffix .py appended. Within a module, the module’s name (as a string) is available as the value of the global variable `__name__`

<br>

> Note
>> For efficiency reasons, each module is only imported once per interpreter session. Therefore, if you change your modules, you must restart the interpreter – or, if it’s just one module you want to test interactively, use importlib.reload(), e.g. import importlib; importlib.reload(modulename). 

<br>

> When you run a Python module with `python fibo.py <arguments>`, the code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`
- Útil para controlar o que o arquivo faz se é rodado como script ou importado como módulo

<br>

### Importações

<br>

Tomemos por exemplo o seguinte projeto

<br>

<pre>
sound/                     <i>Top-level package</i>
│   __init__.py            <i>Initialize the sound package</i>
|
└─── formats/              <i>Subpackage for file format conversions</i>
│    │   __init__.py
│    │   ...
|
└─── effects/              <i>Subpackage for sound effects</i>
|    |   __init__.py
|    |   echo.py
|    |   surround.py
|    |   ...
|
└─── filters/              <i>Subpackage for filters</i>
|    |   __init__.py
|    |   equalizer.py
|    |   vocoder.py
|    |   ...
</pre>

<br>

Seguem alguns exemplos de importação

<br>

| Importador        | Importado           | Declaração                     | Tipo      |
| :---------------: | :----------------: | :-----------------------------: | :-------: |
| filters.vocoder   | effects.echo       | from sound.effects import echo  | Absoluta  |
| effects.surround  | effects.echo       | from . import echo              | Relativa  |
| effects.surround  | formats            | from .. import formats          | Relativa  |
| effects.surround  | filters.equalizer  | from ..filters import equalizer | Relativa  |

<br>

> Note that relative imports are based on the name of the current module’s package. Since the main module does not have a package, modules intended for use as the main module of a Python application must always use absolute imports.

<br>

### Considerações sobre \_\_main\_\_

<br>

[\_\_main\_\_ - Top-level code environment](https://docs.python.org/3/library/__main__.html)

<br>

## Ambientes virtuais com venv

<br>

> venv will install the Python version from which the command was run (as reported by the --version option). For instance, executing the command with python3.12 will install version 3.12.

<br>

A pasta do ambiente e a pasta do projeto não estão necessariamente relacionadas.

<br>

- Criação do ambiente vritual: `python -m venv name-of-folder`
  - > A common directory location for a virtual environment is .venv. This name keeps the directory typically hidden in your shell and thus out of the way while giving it a name that explains why the directory exists.
  - Você pode criar um `.venv` dentro do seu projeto
- Ativação do ambiente virtual
  - > Activating the virtual environment will change your shell’s prompt to show what virtual environment you’re using, and modify the environment so that running python will get you that particular version and installation of Python.
  - Windows: `name-of-folder\Scripts\activate`
  - Unix ou MacOS: `source name-of-folder/bin/activate`
- Desativação do ambiente virtual: `deactivate`

<br>

## Gerenciando pacotes com pip

<br>

__Supõe-se estar rodando em um ambiente virtual venv e o impacto dos comandos é dentro desse ambiente__

<br>

> By default pip will install packages from the [Python Package Index](https://pypi.org/)

<br>

- Instalação de um pacote
  - Última versão: `python -m pip install package`
  - Versão específica: `python -m pip install package==version-number`
- Atualização de um pacote para última versão: `python -m pip install --upgrade package`
- Desinstalação de um pacote: `python -m pip uninstall package`
- Informações de um pacote: `python -m pip show package`
- Listar pacotes instalados: `python -m pip list`
- Listar pacotes instalados em um formato que `python -m pip install` entenda e salvar em um arquivo `requirements.txt`: `python -m pip freeze > requirements.txt`
- Instalação de todos os pacotes listados em `requirements.txt`: `python -m pip install -r requirements.txt`

<br>

### Mapa do nome de importação para nome de distribuição

<br>

```Python
import importlib.metadata  # or: `import importlib_metadata`

importlib.metadata.packages_distributions()['nome-de-importação']
```

<br>

## Distribuição de pacotes

<br>

[Python Packaging User Guide](https://packaging.python.org/en/latest/)

[Packaging Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/)
