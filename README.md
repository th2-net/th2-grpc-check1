# GRPC Generator Template

## Current supported languages: Java, Python

This tool generates code from `.proto` files and upload constructed packages (`.proto` files with generated code) to desired repositories.

### How to use:
Place your own `.proto` files under `src/main/proto` directory and remove example files (`Foo.proto` and `Bar.proto`).

#### For Java: 
- Edit `publishing` section in `build.gradle` (by default it's published to `shared` dir in project root) file in order to specify the desired repository.

#### For Python
- Edit `package_name` variable in `setup.py`. This will be the name of your package.
You can also edit other parameters of `setup.py` in `setup` function invocation such as: `url`, `author`, `author_email`, `description`, `long_description`. Do not edit the others. 

After all editing you can build everything with `docker`:<br>
```
docker build \ 
-t {image_name}:{image_tag} \ 
--build-arg PYPI_REPOSITORY_URL=URL \ 
--build-arg PYPI_USER=USER \ 
--build-arg PYPI_PASSWORD=PASSWORD
```
Where `URL`, `USER`, `PASSWORD` are parameters for publishing Python part.


#### `Publishing` section example for `build.gradle` file:
```
publishing {
    publications {
        mavenJava(MavenPublication) {
            from components.java

            groupId = 'com.exactpro'
            artifactId = 'grpc-check1'
            version = '1.0'

        }
    }
    repositories {
        maven {
            credentials {
                username Username
                password Password
            }
            url RepositoryURL
        }
    }
}
```