# 3D Rotation on Parallel X,Y and Z Axes

### Description
This project, completed as part of the coursework at the Benemérita Universidad Autónoma de Puebla, focuses on rotating a 3D pyramid along the Y and Z axes using parallel rotation. The aim is to apply matrix transformations to rotate a 3D object in space, enhancing the understanding of 3D graphics and transformations.

### Overview
Rotating a vertex in 3D space involves altering its components along the x, y, and z axes. This project specifically targets rotations around the Y and Z axes using parallel rotation techniques. The implementation uses matrix multiplication to perform the necessary transformations.

### Objectives
- Implement parallel rotation for a 3D pyramid using matrix transformations in OpenGL.
- Apply learned concepts to rotate the pyramid around the Y and Z axes.
- Develop an understanding of 3D rotations and their applications in computer graphics.

### Key Features
- **Initialization**: Set up the OpenGL environment and window properties.
- **Rotation Functions**: Implement functions for rotating the pyramid around the Y and Z axes.
- **Matrix Operations**: Utilize matrix multiplication for applying transformations.
- **Animation Loop**: Continuously apply rotations to animate the 3D pyramid.

### Project Structure
The project includes the following main components:

#### Initialization
This function sets up the OpenGL environment, defining the color of the window and the projection parameters.

```cpp
void init(void) {
    glClearColor(0.0, 0.0, 0.0, 1.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(60, 1.0, 1.0, 30.0);
    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity();
    glTranslatef(0.0, 0.0, -3.0);
}
```

#### Parallel Rotation

This function handles the parallel rotation of the pyramid along the specified axis. It first translates the pyramid, performs the rotation, and then translates it back.

```cpp
void Operaciones3D::RotacionParalela(char eje, float theta, float distA, float distB) {
    switch (eje) {
        case 'X': // Parallel rotation around X-axis
            translate(0, -distA, -distB);
            rotateX(DegToRad(theta));
            MultM(R, T, A);
            translate(0, distA, distB);
            MultM(T, A, A);
            break;
        case 'Y': // Parallel rotation around Y-axis
            translate(0, -distA, -distB);
            rotateY(DegToRad(theta));
            MultM(R, T, A);
            translate(0, distA, distB);
            MultM(T, A, A);
            break;
        case 'Z': // Parallel rotation around Z-axis
            translate(0, -distA, -distB);
            rotateZ(DegToRad(theta));
            MultM(R, T, A);
            translate(0, distA, distB);
            MultM(T, A, A);
            break;
    }
}
```

#### Translation Function

This function applies a translation to the 3D object by modifying its coordinates.

```cpp
void translate(float dx, float dy, float dz) {
    float T[4][4] = {
        {1, 0, 0, dx},
        {0, 1, 0, dy},
        {0, 0, 1, dz},
        {0, 0, 0, 1}
    };
    MultM(R, T, A);
}
```

#### Rotation Functions

These functions define the rotation matrices for the X, Y, and Z axes and multiply them with the transformation matrix.

```cpp
void rotateX(float theta) {
    float R[4][4] = {
        {1, 0, 0, 0},
        {0, cos(theta), -sin(theta), 0},
        {0, sin(theta), cos(theta), 0},
        {0, 0, 0, 1}
    };
    MultM(T, R, A);
}

void rotateY(float theta) {
    float R[4][4] = {
        {cos(theta), 0, sin(theta), 0},
        {0, 1, 0, 0},
        {-sin(theta), 0, cos(theta), 0},
        {0, 0, 0, 1}
    };
    MultM(T, R, A);
}

void rotateZ(float theta) {
    float R[4][4] = {
        {cos(theta), -sin(theta), 0, 0},
        {sin(theta), cos(theta), 0, 0},
        {0, 0, 1, 0},
        {0, 0, 0, 1}
    };
    MultM(T, R, A);
}
```

#### Matrix Multiplication Function

This function multiplies two 4x4 matrices.

```cpp
void MultM(float A[4][4], float B[4][4], float C[4][4]) {
    for (int i = 0; i < 4; i++) {
        for (int j = 0; j < 4; j++) {
            C[i][j] = 0;
            for (int k = 0; k < 4; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}
```

### Execution

The project initializes a graphical window and applies parallel rotations to the pyramid along the Y and Z axes. The rotation is continuous, providing a dynamic visual representation of the 3D transformations.

#### X Axis

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/5c7d5474-0e20-444c-bf29-87825f1ae9f4" style="width: 70%; height: auto;">
</p>

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/9a4d3512-7f3b-4e2c-a933-68cffec013d1" style="width: 70%; height: auto;">
</p>

#### Y Axis

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/7ab02664-9f5f-4ca7-ba5c-da0dc9608baf" style="width: 70%; height: auto;">
</p>

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/07f0ac77-6cf3-488b-bcf3-88c3424b99a3" style="width: 70%; height: auto;">
</p>

#### Z Axis

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/be803370-2c47-49df-805e-c5edd4d1431a" style="width: 70%; height: auto;">
</p>

<p align= "center">
    <img src="https://github.com/KPlanisphere/binary-tree-operations/assets/60454942/d0438b6c-3b0f-436f-baa1-29dde8b1dc6e" style="width: 70%; height: auto;">
</p>
