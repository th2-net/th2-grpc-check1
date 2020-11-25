# GRPC Check1 Library

This library contains proto messages and service with RPC methods that are used in [check1](https://github.com/th2-net/th2-check1 "check1") component of th2. 
Tool generates code from `.proto` files and upload built packages (`.proto` files and generated code) to specified repositories.

## How to use:
1. Create a directory with the same name as project name (use underscores instead of dashes) under `src/main/proto` directory (remove other files and directories if they exist).
2. Place your custom `.proto` files in created directory. Pay attention to `package` specifier and `import` statements.
3. Edit `release_version` and `vcs_url` properties in `gradle.properties` file. This are parameters for Java package publication.
4. Edit `rootProject.name` variable in `settings.gradle` file. This will be the name of Java package.
5. Edit `package_info.json` file in order to specify name and version for Python package (create file if it's absent).
6. Edit parameters of `setup.py` in `setup` function invocation such as: `author`, `author_email`, `url`. Do not edit the others.

Note that the name of created directory under `src/main/proto` directory is used in Python (it's a package name).

### Java
If you wish to manually create and publish package for Java, run these command:
```
gradle --no-daemon clean build publish artifactoryPublish \
       -Pbintray_user=${BINTRAY_USER} \
       -Pbintray_key=${BINTRAY_KEY}
```
`BINTRAY_USER` and `BINTRAY_KEY` are parameters for publishing.

### Python
If you wish to manually create and publish package for Python, run these commands:
```
pip install -r requirements.txt
python setup.py generate
python setup.py sdist
twine upload --repository-url ${PYPI_REPOSITORY_URL} --username ${PYPI_USER} --password ${PYPI_PASSWORD} dist/*
```
`PYPI_REPOSITORY_URL`, `PYPI_USER` and `PYPI_PASSWORD` are parameters for publishing.
