# Actualización usando WindUp

> basado en https://windup.github.io/blog/javax-jakarta-openrewrite-automigrate/
> downloads en https://windup.github.io/downloads/

1. Instalar el plugin de WindUp. El CLI se descarga automáticamente.

2. Modificar el `windup-cli`

    ```
    # en la terminal
    code /home/gitpod/.windup/tooling/vscode/windup-cli-6.2.5.Final/bin/windup-cli
    ```

    Modificar la asignación de la variable JAVAVER en la línea 221
    ```
    # antes
    # JAVAVER=`"$JAVACMD" -version 2>&1 | head -n 1 | cut -d '"' -f2`
    JAVAVER="11"
    ```

3. Configurar las opciones en Windup
    - `--input` : `/workspace/jakartaee-duke/complete-duke`
    - `--target` : `jakarta-ee`
    - `--JAVA_HOME` : `/home/gitpod/.sdkman/candidates/java/11.0.26.fx-zulu`

4. Ejecutar el análisis

5. Posibilidad de ejecutar *Quickfixes*

6. Usar recetas de OpenRewrite

    Se pueden ver las recetas en `/home/gitpod/.windup/tooling/vscode/windup-cli-6.2.5.Final/rules/openrewrite/`

    ```
    export WORKSPACE_DIR=/workspace/jakartaee-duke/
    export WINDUP_DIR=/home/gitpod/.windup/tooling/vscode/windup-cli-6.2.5.Final/
    ```

    ```
    sdk use java 11.0.26.fx-zulu
    ```

    ```
    $WINDUP_DIR/bin/windup-cli \
        --openrewrite "-DactiveRecipes=org.jboss.windup.JavaxToJakarta"  \
        "-Drewrite.configLocation=$WINDUP_DIR/rules/openrewrite/jakarta/javax/imports/rewrite.yml" \
        --input $WORKSPACE_DIR/complete-duke/  \
        --goal run
    ```

    ```
    $WINDUP_DIR/bin/windup-cli \
        --openrewrite "-DactiveRecipes=org.jboss.windup.jakarta.javax.PersistenceXml" \
        "-Drewrite.configLocation=$WINDUP_DIR/rules/openrewrite/jakarta/javax/xml/rewrite.yml" \
        --input $WORKSPACE_DIR/complete-duke/  \
        --goal run
    ```    

    ```    
    $WINDUP_DIR/bin/windup-cli \
        --openrewrite "-DactiveRecipes=org.jboss.windup.jakarta.javax.BootstrappingFiles" \ 
        "-Drewrite.configLocation=$WINDUP_DIR/rules/openrewrite/jakarta/javax/bootstrapping/rewrite.yml" \
        --input $WORKSPACE_DIR/complete-duke/  \
        --goal run
    ```        
