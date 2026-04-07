classDiagram

%% =======================
%% USUARIOS Y ROLES
%% =======================

class Usuario {
    +UUID id
    +String nombre
    +String apellido
    +String email
    +String passwordHash
    +Rol rol
    +String fotoPerfil
    +registrar()
    +login()
    +actualizarPerfil()
}

class Rol {
    <<enumeration>>
    ALUMNO
    ENTRENADOR
}

%% =======================
%% ENTRENAMIENTO
%% =======================

class Sesion {
    +UUID id
    +Date fecha
    +String notas
    +crear()
    +editar()
    +eliminar()
}

class Entrada {
    +UUID id
    +String ejercicio
    +Float kilos
    +Int repeticiones
    +Int orden
    +agregar()
    +editar()
    +eliminar()
}

%% =======================
%% ANALITICA / REPORTES
%% =======================

class ResumenEntrenamiento {
    +Date fechaInicio
    +Date fechaFin
    +Int totalSesiones
    +Float totalKilos
    +generarSemanal(usuarioId)
    +generarMensual(usuarioId)
}

class GraficoEvolucion {
    +String ejercicio
    +List~Float~ pesos
    +List~Int~ repeticiones
    +generarDatos(usuarioId, ejercicio)
}

%% =======================
%% RELACIONES
%% =======================

Usuario --> Rol : tiene
Usuario "1" --> "0..*" Sesion : gestiona
Sesion "1" --> "1..*" Entrada : contiene

Usuario "1" --> "0..*" ResumenEntrenamiento : consulta
Usuario "1" --> "0..*" GraficoEvolucion : visualiza

ResumenEntrenamiento --> Sesion : analiza
GraficoEvolucion --> Entrada : analiza
