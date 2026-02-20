
# Pruebas JUnit con Mockito - Guía Completa

## Descripción General
Este repositorio contiene ejemplos de pruebas unitarias utilizando JUnit y Mockito en un proyecto Maven.

## Construcción del Entorno Maven

### Windows 11
#### 1. Instalación de Maven
```bash
# Descargar desde https://maven.apache.org/download.cgi
# Extraer en C:\apache-maven-3.9.x

# Agregar a Variables de Entorno del Sistema
MAVEN_HOME=C:\apache-maven-3.9.x
Path=%MAVEN_HOME%\bin

# Verificar instalación
mvn --version
```

#### 2. Crear Proyecto Maven
```bash
# En C:\Proyectos o ruta deseada
mvn archetype:generate -DgroupId=com.ende -DartifactId=pruebasJUnit -DarchetypeArtifactId=maven-archetype-quickstart

cd pruebasJUnit
```

#### 3. Configuración en VSCode
- Instalar extension: "Extension Pack for Java" (Microsoft)
- Instalar extension: "Maven for Java" (Microsoft)

### Ubuntu 24
#### 1. Instalación de Maven
```bash
# Usando apt
sudo apt update
sudo apt install maven

# O descargar manualmente
cd /home/usuario
wget https://archive.apache.org/dist/maven/maven-3/3.9.x/binaries/apache-maven-3.9.x-bin.tar.gz
tar -xzf apache-maven-3.9.x-bin.tar.gz
echo "export PATH=/home/usuario/apache-maven-3.9.x/bin:$PATH" >> ~/.bashrc
source ~/.bashrc

# Verificar instalación
mvn --version
```

#### 2. Crear Proyecto Maven
```bash
# En /home/usuario/proyectos o ruta deseada
mvn archetype:generate -DgroupId=com.ende -DartifactId=pruebasJUnit -DarchetypeArtifactId=maven-archetype-quickstart

cd pruebasJUnit
```

#### 3. Configuración en VSCode
- Instalar extension: "Extension Pack for Java" (Microsoft)
- Instalar extension: "Maven for Java" (Microsoft)

### Estructura de Directorios Generada
```
pruebasJUnit/
├── pom.xml
├── src/
│   ├── main/java/com/ende/
│   └── test/java/com/ende/
└── target/
```

## Configuración del Entorno Maven

### POM.xml - Dependencias Necesarias
```xml
<dependencies>
    <!-- JUnit 4 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
    
    <!-- Mockito -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>5.2.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Paso a Paso del Código

### 1. Clase Principal a Probar
```java
public class EndePrueba6Feb {
    public int sumar(int a, int b) {
        return a + b;
    }
}
```

### 2. EndePrueba6FebTest.java
```java
@RunWith(MockitoJUnitRunner.class)
public class EndePrueba6FebTest {
    
    @InjectMocks
    private EndePrueba6Feb endePrueba;
    
    @Test
    public void testSumar() {
        assertEquals(5, endePrueba.sumar(2, 3));
    }
}
```

### 3. MockEndePrueba6FebTest.java
```java
@RunWith(MockitoJUnitRunner.class)
public class MockEndePrueba6FebTest {
    
    @Mock
    private Dependencia dependencia;
    
    @InjectMocks
    private EndePrueba6Feb endePrueba;
    
    @Test
    public void testConMock() {
        when(dependencia.getValue()).thenReturn(10);
        assertEquals(10, dependencia.getValue());
    }
}
```

## Pruebas Unitarias

### ¿Por qué Mockito Estático?
- Simplifica la sintaxis con `staticMockito`
- Evita importaciones repetidas
- Mejora legibilidad del código de pruebas

### Pasos de Ejecución
```bash
# Compilar
mvn clean compile

# Ejecutar todas las pruebas
mvn clean test

# Ejecutar prueba específica
mvn test -Dtest=EndePrueba6FebTest

# Empaquetar
mvn package
```
